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

def generate_unique_names():
    # Create a pool of characters: A-Z, 0-9

    characters = 'abcdefghijklmnopqrstuvwxyz0123456789'
    
    # Generate all combinations of 4 characters
    unique_names = [''.join(comb) for comb in itertools.product(characters, repeat=4)]
    
    return unique_names

# Example usage
unique_names = generate_unique_names()

# Print the first 10 unique names
characters = 'abcdefghijklmnopqrstuvwxyz0123456789'
print([''.join(comb) for comb in itertools.product(characters, repeat=4)])



shutil.copyfile("old_path/" + old_name + ".pdb", "new_path/" + new_name + ".pdb")

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