## DaliLite.V5 usage

> http://ekhidna2.biocenter.helsinki.fi/dali/README.v5.html


```
../bin/dali.pl 
--cd1 2nrmA  # --cd1 <xxxxX>             query structure identifier
--db pdb.list #--db <filename>           list of target structure identifiers
--TITLE systematic 
--dat1 ../DAT # path to directory containing query data [default: ./DAT/]
--dat2 ../DAT # path to directory containing target data [default: ./DAT/]
> systematic.stdout 
2> systematic.stderr

```

## dali name assignment

```python

import itertools
import os, gzip, shutil

## roginal name 2 daliname
def generate_unique_names():
    # Create a pool of characters: A-Z, 0-9
    characters = 'abcdefghijklmnopqrstuvwxyz0123456789'
    # Generate all combinations of 4 characters
    unique_names = [''.join(comb) for comb in itertools.product(characters, repeat=4)]
    return unique_names

unique_names = generate_unique_names()

orginalPDB_path = "./PDB/"
orginalPDB_fps = glob.glob(os.path.join(orginalPDB_path, "*.pdb"))
daliPDB_path = "./daliPDB/"

orig2dali_rows = [] 

for i in range(len(orginalPDB_fps)):
    fp = orginalPDB_fps[i]
    origname = fp.split("\\")[-1]
    daliname = unique_names[i]
    row = {"orginalPDB":origname, "daliPDB":daliname}
    orig2dali_rows.append(row)

orig2dali_df = pd.DataFrame(orig2dali_rows)
orig2dali_df.to_csv("orig2dali_df.csv")

shutil.copyfile(fp, daliPDB_path + daliname + ".pdb")

```


## usage history

```
#!/bin/bash


module load blast/2.11.0+

# cd /(...)/lihuilin/myDali/DaliLite.v5/xxx_ALL/
# dat_dir="omg_xxx_dir"
# ls $dat_dir | perl -pe 's/\.dat//' > $dat_dir.list
# sys_dir="omg_xxx_sysm"
# mkdir -p "$sys_dir"
# cd $sys_dir
# ../../bin/dali.pl -cd1 0000A --db ../$dat_dir.list --TITLE sysm --dat1 ../$dat_dir --dat2 ../$dat_dir

for rep in aanwA bbydA bbx7A aafwA bbx4A bbyqA aabhA bbx5A bbx6A bbnuA
do
    cd /(...)/lihuilin/myDali/DaliLite.v5/xxx_ALL/
    dat_dir=$rep"_dat"
    ls $dat_dir | perl -pe 's/\.dat//' > $dat_dir.list
    sys_dir=$rep"_sysm"
    mkdir -p "$sys_dir"
    cd $sys_dir
    ../../bin/dali.pl -cd1 0000A --db ../$dat_dir.list --TITLE sysm --dat1 ../$dat_dir --dat2 ../$dat_dir
done


#../../bin/dali.pl -cd1 0000A --db ../xxxpdbR1.list --TITLE xxx_sysm --dat1 ../xxxDAT1 --dat2 ../xxxDAT1

```


```
#!/bin/bash

cd /storage/shenhuaizhongLab/lihuilin/myDali/DaliLite.v5/YYY_ALL

module load blast/2.11.0+


# mkdir -p "omg_fbp_dir"
# for file in ./*.pdb; do
#     id=$(basename $file .pdb | head -c 4)
#     ../bin/import.pl --pdbfile $file --pdbid $id --dat omg_fbp_dir --clean
# done

for rep in chunk1 chunk2 chunk3 chunk4 chunk5
do
    dat_dir=$rep"_dat"
    mkdir -p "$dat_dir"
    ../bin/import.pl --pdbfile ./0000A.pdb --pdbid 0000 --dat $dat_dir --clean
    for file in $rep/*.pdb; do
        id=$(basename $file .pdb | head -c 4)
        ../bin/import.pl --pdbfile $file --pdbid $id --dat $dat_dir --clean
    done
done

```