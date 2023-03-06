# Tutorial using PLANTS (Protein-Ligand ANTSystem) version 1.2
Preparation
1. Separate protein, ligand and water using spores with the command:`spores --mode splitpdb 3htb.pdb`
2. Later you will get a file with the protein with the name protein.mol2 and the ligand with the name ligand_JZ4167_0.mol2
3. Open file protein.mol2 in the chimera, Tools > Structure Editing > Dock Prep > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and standard residues > File > Save PDB > overwrite the rec.mol2 file
4. Open ligand in chimera, Tools > Structure Editing > Dock Prep > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and nonstandard residues > File > Save PDB > overwrite file lig.mol2
5. Add protonation using: `spores --mode protstates lig.mol2 ligprotonated.mol2`
4. Determine the binding site definition with the command: `plants --mode bind lig.mol2 rec.mol2`
5. Copy info bindingsite_center and bidingsite_radius into dock.txt:
<br> `bindingsite_center 22.7142 -25.2627 -3.283` <br> `bindingsite_radius 3.75624`
6. Run molecular docking with the command:
`plants --mode screen dock.txt`


