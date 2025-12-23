# PyMol

 - select residues based on residue number
```t
select nterm, resi 42+74+43+56+39
```
- mutate one amino acid
```t
cmd.wizard("mutagenesis")
cmd.fetch("target.pdb")
cmd.get_wizard().set_mode("LEU")
cmd.get_wizard().do_select("chain A and resid 22")
cmd.get_wizard().apply()
cmd.save("mutated_target.pdb")
```
- save as .pdb file.
```
File > Export Structure > Export Molecule > Save > change "save as type"
```

- diagram
    - Space-filling diagram:
        - shows all atoms
    - Ribbon/Cartoon diagram:
        - shows the protein backbone and highlights the alpha helices.
    - Surface diagram:
        - shows areas that are accessible to water molecules.
<center>
  <figure>
    <img src="./img/protein_vis.png" alt=" " >
    <figcaption>ref: https://pdb101.rcsb.org/learn/videos </figcaption>
  </figure>
</center>
