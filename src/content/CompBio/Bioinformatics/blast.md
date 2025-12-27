## sequence alignment via BLASTp with using makeblastdb for custom database


```
module load blast/2.11.0+

makeblastdb -in ./targetDB/target30.fasta -input_type fasta -dbtype prot -out ./targetDB_blast/targetDB.blast

blastp -query q92508.fasta -db ./targetDB_blast/targetDB.blast -outfmt 5 -out query_blastp_target30_fmt5.xml

tree
.
├── q92508.fasta
├── query_blastp_target30_fmt5.xml
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

- paese
```
from Bio.Blast import NCBIXML

with open("./query_blastp_target30_fmt5.xml") as f:
    records = NCBIXML.parse(f)
    for record in records:
        for alignment in record.alignments:
            print("Target:", alignment.hit_def)
            for hsp in alignment.hsps:
                print("  Score:", hsp.score)
                print("  E-value:", hsp.expect)
                print("  Query seq:", hsp.query)
                print("  Sbjct seq:", hsp.sbjct)
                print("  Match:", hsp.match)

```
