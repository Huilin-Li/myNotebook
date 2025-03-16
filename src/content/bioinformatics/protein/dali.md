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