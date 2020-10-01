Data is present @ home5/pthunga/consultingProject/run1 home5/pthunga/consultingProject/run2
### Rename files 

All files were renamed to include run information. Since everything was run on the same lane, lane info was removed. 
4 libraries in total(Bay1, Bay2, LB1, LB2). Paired end reads (n01 or n02). All libraries were run two times (R1 and R2)

```bash
#script name: rename.sh
#/bin/bash

WORKDIR=$1
run=$2
cd ${WORKDIR}

for file in *Bay*;
do
        sample=${file: -18}
 #      run="R1"
        newName="$run$sample"
mv $file ${WORKDIR}/$newName;

done

for file in *LB*;
do
        sample=${file: -17}
       # run="R1"
        newName="$run$sample"
mv $file ${WORKDIR}/$newName;

done

### call this script using: ./rename.sh /path/to/file <insert run #>
```
### Quality Control

Fastqc(version v0.11.8) on the cluster didn't work. Throws this java runtime error: (The full log is saved under the qcReport directory)

```
JRE version: OpenJDK Runtime Environment (9.0) (build 9-internal+0-2016-04-14-195246.buildd.src)
# Java VM: OpenJDK 64-Bit Server VM (9-internal+0-2016-04-14-195246.buildd.src, mixed mode, tiered, compressed oops, g1 gc, linux-amd64)
# Problematic frame:
# C  [libjava.so+0x1d009]  JNU_GetEnv+0x19
 ```
 Installed and unzipped v0.11.9 @ /home5/pthunga/consultingProject/packages
 
 ```bash
#script name: qc.sh
#/bin/bash

#code to run QC

export PATH=/usr/lib/jvm/java-8-oracle/jre/bin:$PATH
#export PATH=usr/local/bin/FastQC:$PATH
WORKDIR=$1
OUTDIR=$2
#declare -a fwdArray=($(ls ${WORKDIR}/R*))
#arrayLength=${#fwdArray[*]}
cd ${WORKDIR}

for file in R*;
do
      /home5/pthunga/consultingProject/packages/FastQC/fastqc ${WORKDIR}/$file -o ${OUTDIR};
done

### call this script using: ./qc.sh /path/to/data /path/to/outputdir
 ```
 weirdly, this doesn't work if I sbatch it. Looks like some kind of a path or permission issue. I've emailed Chris to see how I can fix it. 
 
 Chris' response:
 >When you submit a script to slurm using sbatch, slurm copies that script to the node on which it will run. It copies it to a slurm-specific directory at /var/lib/slurm-llnl/slurmd/jobNNNNN where NNNNN is the slurm job number. By default the fastqc (Perl) script sets the Java CLASSPATH variable from the location of the fastqc script itself, so when you run fastqc directly through sbatch the CLASSPATH is set to be /var/lib/slurm-llnl/... which is not at all where the Java class code is found.
 
(That makes sense, figure out where to put sbatch -- within or outside script)

QC reports are present @ /home5/pthunga/consultingProject/qcReport. There should be a multiqc report somewhere in that directory. 

Looks like there is some nextera adapter contamination.

### Trimming

Using Trimgalore 
```bash
#script name: trim.sh
#/bin/bash

export PATH="home5/pthunga/consultingProject/packages/TrimGalore-0.6.6:$PATH"
WORKDIR=$1
cd ${WORKDIR}

declare -a fwdArray=($(ls ${WORKDIR}/R*n01*))
declare -a revArray=($(ls ${WORKDIR}/R*n02*))
arrayLength=${#fwdArray[*]}

for (( i=0; i<${arrayLength}; i++ ));
do
    sbatch trim_galore --paired --nextera  ${fwdArray[$i]} ${revArray[$i]}
done

#call script using ./trim.sh /path/to/data 
```


