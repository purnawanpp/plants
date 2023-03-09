# Tutorial using Protein-Ligand ANTSystem (PLANTS) version 1.2

### Software Requaired and link to download:
1. [Spores](http://www.tcd.uni-konstanz.de/plants_download/) 
2. [Plants](http://www.tcd.uni-konstanz.de/plants_download/)
3. [Openbabel](https://github.com/openbabel/openbabel)
4. [Chimera](https://www.cgl.ucsf.edu/chimera/download.html)

### Software Installation:
1. `chmod +x spores`
2. `chmod +x plants`
3. `./spores`
4. `./plants`
5. Create a [path](https://gist.github.com/nex3/c395b2f8fd4b02068be37c961301caa7) to make it easier to use in the terminal 

## OPSI 1-Molecular Docking using google colab
1. Please run this command in google colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/purnawanpp/plants/blob/main/plants.ipynb)

## OPSI 2-Tutorial using Protein-Ligand ANTSystem (PLANTS) and Structure PrOtonation and REcognition System  (SPORES)
### Preparation and Molecular Docking
1. Separate protein, ligand and water using spores with the command:`spores --mode splitpdb 3htb.pdb`
2. Later you will get a file with the protein with the name **protein.mol2** and the ligand with the name **ligand_JZ4167_0.mol2**
3. Add structure recognition, protonation and generates all combinatorial possible protonation states of the input molecule: `spores --mode protstates ligand_JZ4167_0.mol2 ligprotonated.mol2`
6. Determine the *binding_site* definition with the command: `plants --mode bind ligand_JZ4167_0.mol2 protein.mol2`
7. Copy info bindingsite_center and bidingsite_radius into [dock.txt](https://github.com/purnawanpp/plants/blob/main/dock.txt):
<br> `bindingsite_center 22.7142 -25.2627 -3.283` <br> `bindingsite_radius 3.75624`
8. Run molecular docking with the command:
`plants --mode screen dock.txt`
9. Open the output folder, there will be a file with the name bestranking.csv in that information. The Total Score is the result of the free energy calculation as a result of molecular docking
10. Calculation RMSD run this command (Warning! */mnt/d/Software/PLANTS/kuy/results/* is path of folder): 
<br>`obrms -f lig.mol2 /mnt/d/Software/PLANTS/kuy/results/lig.pdb_entry_00001_conf_01.mol2`

### Meaning input in [dock.txt](https://github.com/purnawanpp/plants/blob/main/dock.txt):
1. `scoring_function chemplp`: determines the type of scoring function used, in this case using ChemPLP.
2. `search_speed speed1`: determines the search speed used, in this case using speed1.
3. `protein_file rec.mol2`: specifies the protein file that will be used as the docking target.
4. `ligand_file ligprotonated.mol2`: specifies the ligand file that will be docked to the protein.
5. `output_dir results`: specifies the folder where the output results will be stored.
6. `write_multi_mol2 0`: determines whether the docking results will be saved in a single file or multiple files. If set to 0, the docking results will be saved in a single file.
7. `bindingsite_center 22.7142 -25.2627 -3.283`: determines the center coordinates of the binding site between the protein and the ligand.
8. `bindingsite_radius 3.75624`: determines the radius of the binding site between the protein and the ligand.
9. `cluster_structures 10`: determines the number of docked structures that will be clustered.
10. `cluster_rmsd 2.0`: determines the maximum RMSD value allowed for structures to be clustered. Structures with an RMSD value lower than this value will be clustered together.

### OPSI 3-Tutorial using Protein-Ligand ANTSystem (PLANTS) and Chimera
### Preparation and Molecular Docking
1. Separate protein, ligand and water using spores with the command:`spores --mode splitpdb 3htb.pdb`
2. Later you will get a file with the protein with the name **protein.mol2** and the ligand with the name **ligand_JZ4167_0.mol2**
3. Open file **protein.mol2** in the chimera, Tools > Structure Editing > Dock Prep > Ok > Ok > On Assign Charges for dock prep click Gasteiger and standard residues > File > Save PDB > save file namely **rec.mol2** file
4. Open **ligand_JZ4167_0.mol2** in chimera, Tools > Structure Editing > Dock Prep > Ok > Ok > On Assign Charges for dock prep click Gasteiger and nonstandard residues > File > Save PDB > save file namely **lig.mol2**
5. Add structure recognition, protonation and generates all combinatorial possible protonation states of the input molecule: `spores --mode protstates lig.mol2 ligprotonated.mol2`
6. Determine the *binding_site* definition with the command: `plants --mode bind lig.mol2 rec.mol2`
7. Copy info bindingsite_center and bidingsite_radius into [dock.txt](https://github.com/purnawanpp/plants/blob/main/dock_opsi3.txt):
<br> `bindingsite_center 22.7142 -25.2627 -3.283` <br> `bindingsite_radius 3.75624`
8. Run molecular docking with the command:
`plants --mode screen dock.txt`
9. Open the output folder, there will be a file with the name bestranking.csv in that information. The Total Score is the result of the free energy calculation as a result of molecular docking
10. Calculation RMSD run this command (Warning! */mnt/d/Software/PLANTS/kuy/results/* is path of folder): 
<br>`obrms -f lig.mol2 /mnt/d/Software/PLANTS/kuy/results/lig.pdb_entry_00001_conf_01.mol2`

### Meaning input in [dock_opsi3.txt](https://github.com/purnawanpp/plants/blob/main/dock_opsi3.txt):
1. `scoring_function chemplp`: determines the type of scoring function used, in this case using ChemPLP.
2. `search_speed speed1`: determines the search speed used, in this case using speed1.
3. `protein_file rec.mol2`: specifies the protein file that will be used as the docking target.
4. `ligand_file ligprotonated.mol2`: specifies the ligand file that will be docked to the protein.
5. `output_dir results`: specifies the folder where the output results will be stored.
6. `write_multi_mol2 0`: determines whether the docking results will be saved in a single file or multiple files. If set to 0, the docking results will be saved in a single file.
7. `bindingsite_center 22.7142 -25.2627 -3.283`: determines the center coordinates of the binding site between the protein and the ligand.
8. `bindingsite_radius 3.75624`: determines the radius of the binding site between the protein and the ligand.
9. `cluster_structures 10`: determines the number of docked structures that will be clustered.
10. `cluster_rmsd 2.0`: determines the maximum RMSD value allowed for structures to be clustered. Structures with an RMSD value lower than this value will be clustered together.



### Reference:
1. https://github.com/purnawanpp/plants/blob/main/plants_manual1.2.pdf
2. https://github.com/purnawanpp/plants/blob/main/spores_manual.pdf
3. https://github.com/purnawanpp/plants/blob/main/pharmaCO_manual.pdf


