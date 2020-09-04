### Rename file

```bash
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


