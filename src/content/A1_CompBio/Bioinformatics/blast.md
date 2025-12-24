## sequence alignment via BLASTp with using makeblastdb for custom database


```
module load blast/2.11.0+

makeblastdb -in ./targetDB/target30.fasta -input_type fasta -dbtype prot -out ./targetDB_blast/targetDB.blast

blastp -query q92508.fasta -db ./targetDB_blast/targetDB.blast > query_blastp_target30.out

tree
.
├── q92508.fasta
├── query_blastp_target30.out
├── targetDB
│   └── target30.fasta
└── targetDB_blast
    ├── targetDB.blast.pdb
    ├── targetDB.blast.phr
    ├── targetDB.blast.pin
    ├── targetDB.blast.pot
    ├── targetDB.blast.psq
    ├── targetDB.blast.ptf
    └── targetDB.blast.pto


```

