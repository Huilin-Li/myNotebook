## .cif to .pdb

## PyMol
File > Export Structure > Export Molecule > Save > change "save as type"

## SeqIO.parse
```
from Bio import SeqIO

records = SeqIO.parse("input_file.cif", "cif-atom")
SeqIO.write(records, "output_file.pdb", "pdb-atom")
```

## RCSB maxit 
```
maxit -i file.cif -o 2
```
