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