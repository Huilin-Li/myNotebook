# MMseqs2 usage (straightforward)

## usage history

```
#!/bin/bash

cd /(...)/lihuilin/MMseqs2/
cd build

make
make install
export PATH=$(pwd)/bin/:$PATH

# echo "============================================== COMPILE ENVIRONMENT ========================================================="



cd /(...)/lihuilin/myMMseqs2


mmseqs easy-search /(...)/lihuilin/query/xxx_mut.fa /(...)/lihuilin/DB/PDB_UPSP_fasta_DB/faDB.fasta xxx_mut_mmseqs_id_0_2_c_0_7.m8 tmp --min-seq-id 0.2 -c 0.7 --format-output query,target,fident,evalue,bits,qheader,theader,tseq


# echo "============================================== .pdb file of these similar sequence ========================================================="
result_file="/(...)/lihuilin/myMMseqs2/xxx_mut_mmseqs_id_0_2_c_0_7.m8"
PDBdb_dir="/(...)/lihuilin/DB/pure_PDB_DB_by_Chain/"
AFDBdb_dir="/(...)/lihuilin/DB/AFDB_pLDDT_70"

output_dir="/(...)/lihuilin/myMMseqs2/xxx_mut_mmseqs_id_0_2_c_0_7_pdb_dir"
mkdir -p "$output_dir"


AFDB_pLDDT_70_log="/(...)/lihuilin/DB/AFDB_pLDDT_70.log"
pure_PDB_DB_by_Chain_log="/(...)/lihuilin/DB/pure_PDB_DB_by_Chain.log"


while read -r line; do
    ID=$(echo "$line" | awk '{print $2}')
    echo "$ID"
    if grep -q "$ID.pdb" $pure_PDB_DB_by_Chain_log; then
        inp_fp="$PDBdb_dir$ID.pdb"
        oup_fp="$output_dir/$ID.pdb"
        cp "$inp_fp" "$oup_fp"
    elif grep -q "AF-$ID.pdb" $AFDB_pLDDT_70_log; then
        inp_fp="$AFDBdb_dir/AF-$ID.pdb"
        oup_fp="$output_dir/AF-$ID.pdb"
        cp "$inp_fp" "$oup_fp"
    else
        echo "didnt download $ID structure"
    fi
done < $result_file




```


## multiple seqs search

```
#!/bin/bash

cd /(...)/lihuilin/MMseqs2/
cd build

make
make install
export PATH=$(pwd)/bin/:$PATH

windowsfa="/(...)/lihuilin/query/xxx_mut_windows.fa"
m8fp="/(...)/lihuilin/myMMseqs2/xxx_mut_windows_mmseqs.m8"
mmseqs easy-search $windowsfa /(...)/lihuilin/DB/PDB_UPSP_fasta_DB/faDB.fasta $m8fp tmp --format-output query,target,fident,evalue,nident,alnlen,mismatch,qstart,qend,tstart,tend,bits,qheader,theader,tseq




```