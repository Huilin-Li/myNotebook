# Chapter 4 The Taxonomy Project
> https://www.ncbi.nlm.nih.gov/books/NBK21100/

Each entry in the database is a “taxon”, also referred to as a “node” in the database. The “root node” (taxid1) is at the top of the hierarchy. 

The path from the root node to any other particular taxon in the database is called its “lineage”; the collection of all of the nodes beneath any particular taxon is called its “subtree”. 


> https://ftp.ncbi.nih.gov/pub/taxonomy/

- taxdump.tar.gz
- taxdump.tar.gz.md5

which contain MD5 sums for the corresponding archive files. These files might be used to check correctness of the download of corresponding archive file.

```
gunzip -c taxdump.tar.gz | tar xf - 

```

# taxonkit
```
conda install -c bioconda taxonkit

taxonkit lineage beam_tax.txt | tee ./domain_tax/beam_tax_lin.txt
```