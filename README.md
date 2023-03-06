# Tutorial using PLANTS (Protein-Ligand ANTSystem) version 1.2
Preparation and Molecular Docking
1. Separate protein, ligand and water using spores with the command:`spores --mode splitpdb 3htb.pdb`
2. Later you will get a file with the protein with the name *protein.mol2* and the ligand with the name *ligand_JZ4167_0.mol2*
3. Open file protein.mol2 in the chimera, Tools > Structure Editing > Dock Prep > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and standard residues > File > Save PDB > overwrite the rec.mol2 file
4. Open ligand in chimera, Tools > Structure Editing > Dock Prep > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and nonstandard residues > File > Save PDB > overwrite file lig.mol2
5. Add protonation using: `spores --mode protstates lig.mol2 ligprotonated.mol2`
4. Determine the binding site definition with the command: `plants --mode bind lig.mol2 rec.mol2`
5. Copy info bindingsite_center and bidingsite_radius into dock.txt:
<br> `bindingsite_center 22.7142 -25.2627 -3.283` <br> `bindingsite_radius 3.75624`
6. Run molecular docking with the command:
`plants --mode screen dock.txt`
7. Open the output folder, there will be a file with the name bestranking.csv in that information. The Total Score is the result of the free energy calculation as a result of molecular docking

Meaning input in dock.txt
1. `scoring_function chemplp`: determines the type of scoring function used, in this case using ChemPLP.
2. `search_speed speed1`: determines the search speed used, in this case using speed1.
3. `protein_file rec.mol2`: specifies the protein file that will be used as the docking target.
4. `ligand_file ligprotonated.mol2`: specifies the ligand file that will be docked to the protein.
5. `flexible_protein_side_chain_11`: allows the protein to move flexibly at side positions (we choose active site, please check uniprot).
6. `output_dir results`: specifies the folder where the output results will be stored.
7. `write_multi_mol2 0`: determines whether the docking results will be saved in a single file or multiple files. If set to 0, the docking results will be saved in a single file.
8. `bindingsite_center 22.7142 -25.2627 -3.283`: determines the center coordinates of the binding site between the protein and the ligand.
9. `bindingsite_radius 3.75624`: determines the radius of the binding site between the protein and the ligand.
10. `cluster_structures 10`: determines the number of docked structures that will be clustered.
11. `cluster_rmsd 2.0`: determines the maximum RMSD value allowed for structures to be clustered. Structures with an RMSD value lower than this value will be clustered together.

