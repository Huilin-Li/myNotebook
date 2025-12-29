# alignment in ChimeraX command line


```
import os
from chimerax.core.commands import run

target = r"E:/CLUSTERwork/PIEZO1_EVO/regionSearch/query4regions/blade1_1304.pdb"
inputFolder = r"E:/CLUSTERwork/PIEZO1_EVO/regionSearch/foldseekResults/chimeraX/bladePDB"
outputFolder = r"E:/CLUSTERwork/PIEZO1_EVO/regionSearch/foldseekResults/chimeraX/bladePDBaligned"


run(session, f'open "{target}"')  # #1

for pdb_file in sorted(os.listdir(inputFolder)):

    input_path = os.path.join(inputFolder, pdb_file)
    output_path = os.path.join(outputFolder, pdb_file.replace(".pdb", "_aligned_CA.pdb"))

    run(session, f'open "{input_path}"')        # #2
    run(session, 'mm #2@CA to #1@CA')           # fit using only CA
    run(session, 'select #2@CA')                # keep only CA for saving
    run(session, f'save "{output_path}" models #2 selectedOnly true')
    run(session, 'close #2')                    # free memory

```

In chimeraX
```
runscript "E:/CLUSTERwork/PIEZO1_EVO/regionSearch/foldseekResults/chimeraX/chimeraX.py"
```