# Biopython


### SeqIO.parse()

```python
from Bio import SeqIO

with open("fa.fasta") as fa:
    for record in SeqIO.parse(fa, "fasta"):
        ID = record.id
        seq = record.seq
        description = recrod.description 

```

```python
from Bio import PDB



if __name__=="__main__":
    for pdbfile_path in glob.glob("/path/DB/pure_PDB/*.pdb"):
        name = pdbfile_path.split("\\")[-1].split(".")[0]
        print(name, end=" ")
        pdb = PDB.PDBParser().get_structure(name, pdbfile_path)
        pdb_io = PDB.PDBIO()
        pdb_chains = pdb.get_chains()
        for chain in pdb_chains:
            pdb_io.set_structure(chain)
            pdb_io.save("/path/DB/pure_PDB_DB_by_Chain/" + pdb.get_id() + "_" + chain.get_id() + ".pdb")
        print('-- Done') 
        
```

```python
from Bio import SeqIO

def pdb2fasta(pdb_file, fasta_file, HEADER=None):
    with open(pdb_file, 'r') as pdb_file:
        for record in SeqIO.parse(pdb_file, 'pdb-atom'):
            if '?' in record.id:
                header = HEADER
            else:
                header = record.id
            with open(fasta_file, 'w') as fasta_file:
                fasta_file.write('>' + header+'\n')
                fasta_file.write(str(record.seq))
    return record.seq
```

```python
from Bio import SeqIO

with open('fa.fasta') as fasta_file:  
    identifiers, seq = [], []
    for seq_record in SeqIO.parse(fasta_file, 'fasta'): 
        identifiers.append(seq_record.id)
        seq.append("".join(seq_record.seq))

fa_df = pd.DataFrame()
fa_df["seq"] = seq
fa_df["id"] = identifiers
```

### remove DNA/RNA and O from pdb format
```python
from Bio import PDB


class rm_dna_rna_O(PDB.Select):
    def accept_residue(self, res):
        if (len(res.get_resname()) <3) or (res.id[0] != " "):
            return False
        else:
            return True



if __name__=="__main__":
    for pdbfile_path in glob.glob("/path/PDBDB/*.pdb"):
        print(pdbfile_path, end=" ")
        name = pdbfile_path.split("/")[-1]
        pdb = PDB.PDBParser().get_structure(name, pdbfile_path)
        pdb_io = PDB.PDBIO()
        pdb_io.set_structure(pdb)
        pdb_io.save("/path/PDBDB_no_drna/"+name, rm_dna_rna_O())
        print('-- Done') 
```
        
### remove HETATOM from pdb format 

```python
from Bio import PDB

pdb = PDB.PDBParser().get_structure("2gq1", "FBP/2gq1.pdb")

class ResSelect(PDB.Select):
    def accept_residue(self, res):
        if res.id[0] != " ":  #>= start_res and res.id[1] <= end_res and res.parent.id == chain_id:
            return False
        else:
            return True

pdb_io = PDB.PDBIO()
pdb_io.set_structure(pdb)
pdb_io.save("FBP/2gq1_no_HETATOM.pdb", ResSelect())
```


```python
import os, gzip, shutil
import glob
import numpy as np
import pandas as pd
from Bio import SeqIO

# unzip all .gz files
start_dir = "./ftp.ensembl.org/pub/current_fasta/"
gz_count = []
destination_dir = "./fa_save/"
for root, dirs, files in os.walk(start_dir):
    for gz_name in files:
        gz_file = os.path.join(root, gz_name)
        if "/pep/" in gz_file:
            # print(gz_file)
            gz_count.append(gz_file)
            out_file = destination_dir + gz_name.split(".gz")[0]
            with gzip.open(gz_file,"rb") as f_in, open(out_file,"wb") as f_out:
                shutil.copyfileobj(f_in, f_out)
```
```python
# read
with open("./fa_save/all_data.fa") as fasta_file:
    identifiers = []
    seq = []
    for seq_record in SeqIO.parse(fasta_file, 'fasta'): 
        identifiers.append(seq_record.id)
        seq.append("".join(seq_record.seq))
df_pro = pd.DataFrame()
df_pro["aa_seq"] = seq
df_pro["p_id"] = identifiers
# clear duplicates
df_pro_drop_dup = df_pro.drop_duplicates(subset='aa_seq')
```
