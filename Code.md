Data is present @ home5/pthunga/consultingProject/run1 home5/pthunga/consultingProject/run2
### Rename files 

All files were renamed to include run information. Since everything was run on the same lane, lane info was removed. 
4 libraries in total(Bay1, Bay2, LB1, LB2). Each library has a duplicate (n01 or n02). All libraries were run two times (R1 and R2)

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

Fastqc on the cluster didn't work. Throws a java runtime error. 
```
JRE version: OpenJDK Runtime Environment (9.0) (build 9-internal+0-2016-04-14-195246.buildd.src)
# Java VM: OpenJDK 64-Bit Server VM (9-internal+0-2016-04-14-195246.buildd.src, mixed mode, tiered, compressed oops, g1 gc, linux-amd64)
# Problematic frame:
# C  [libjava.so+0x1d009]  JNU_GetEnv+0x19
 ```
 

