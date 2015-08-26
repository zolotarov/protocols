# Docking simulation using AutoDock 4.2

## Requirements

AutoDock 4.2 and AutoDockTools have to be installed.

### Prepare a receptor using AutoDockTools

```bash
/Library/MGLTools/1.5.6/bin/python /Library/MGLTools/1.5.6/MGLToolsPckgs/AutoDockTools/Utilities24/prepare_receptor4.py -r 4iys.pdb -o 4iys.pdbqt -A checkhydrogens
``` 

## Prepare a ligand using AutoDockTools

1. Convert ligand file to PDB using OpenBabel

```bash
babel zinc_20031600.mol2 zinc_20031600.pdb
```

2. Prepare ligand 

```bash
/Library/MGLTools/1.5.6/bin/python /Library/MGLTools/1.5.6/MGLToolsPckgs/AutoDockTools/Utilities24/prepare_ligand4.py -l zinc_20031600.pdb
```

## Create a grid using PyMol and autodock.py (did not work)

Download [plugin](https://github.com/ADplugin/ADplugin)

Rename MacPyMol to PyMOLX11Hybrid to allow the application to run in the X11 mode, which allows the use of plugins.

Set the coordinates of the grid box in pymol and save the file with `.gpf` extension.

**Note: this file did not work with `autorid`.**

## Convert PDB to PDBQT using AutoDockTools

Open the receptor: File → Read Molecule → Select the `.pdb` file → Open

Remove waters: 

1. Select → Select From String → Type HOH* in the Residue box and * in the Atom box → Add → Dismiss
2. Edit → Delete → Delete Selected Atoms → CONTINUE

Add hydrogens: Edit → Hydrogens → Add → All Hydrogens, noBondOrder, yes → OK

Assign AutoDock element field: Edit → Atoms → Assign AD4 type

Compute Gasteiger charges: Edit → Charges → Compute Gasteiger

Save the receptor: File → Save → Write PDBQT → OK


## Create a grid using AutoDockTools

Select Ligand: Ligand → Input → Choose... (will take couple mins)
Select Macromolecule: → Grid → Macromolecule → Choose... → Select Molecule
Make a grid: Grid → Grid Box... and set the coords
Save the grid: Grid → Output → Save GPF...


## Run autogrid

`autogrid4 -p 4iys.gpf`

This will generate atom-specific affinity maps with `.map` extension as well as 2 files `receptor.maps.fld` and `receptor.maps.xyz`, where `receptor` is the name of the protein file, without the `.gpf` extension.

The `.gpf` file needs to modified to include atoms that might be found in ligands, such as chlorine and bromium.

Default `.gpf`:

```
npts 60 60 60                        # num.grid points in xyz
gridfld 4iys.maps.fld                # grid_data_file
spacing 0.375                        # spacing(A)
receptor_types A C HD N NA OA SA     # receptor atom types
ligand_types A C HD N NA OA SA       # ligand atom types
receptor 4iys.pdbqt                  # macromolecule
gridcenter auto                      # xyz-coordinates or auto
smooth 0.5                           # store minimum energy w/in rad(A)
map 4iys.A.map                       # atom-specific affinity map
map 4iys.C.map                       # atom-specific affinity map
map 4iys.HD.map                      # atom-specific affinity map
map 4iys.N.map                       # atom-specific affinity map
map 4iys.NA.map                      # atom-specific affinity map
map 4iys.OA.map                      # atom-specific affinity map
map 4iys.SA.map                      # atom-specific affinity map
elecmap 4iys.e.map                   # electrostatic potential map
dsolvmap 4iys.d.map              # desolvation potential map
dielectric -0.1465                   # <0, AD4 distance-dep.diel;>0, constant
```

Modify to include the grid center, and extra atom type and then run:

```
npts 60 60 60                        # num.grid points in xyz
gridfld 4iys.maps.fld                # grid_data_file
spacing 0.375                        # spacing(A)
receptor_types A C HD N NA OA SA     # receptor atom types
ligand_types A C HD N NA OA SA BR      # ligand atom types
receptor 4iys.pdbqt                  # macromolecule
gridcenter   -19.951   -7.611  -25.596
smooth 0.5                           # store minimum energy w/in rad(A)
map 4iys.A.map                       # atom-specific affinity map
map 4iys.C.map                       # atom-specific affinity map
map 4iys.HD.map                      # atom-specific affinity map
map 4iys.N.map                       # atom-specific affinity map
map 4iys.NA.map                      # atom-specific affinity map
map 4iys.OA.map                      # atom-specific affinity map
map 4iys.SA.map                      # atom-specific affinity map
map 4iys.BR.map
elecmap 4iys.e.map                   # electrostatic potential map
dsolvmap 4iys.d.map              # desolvation potential map
dielectric -0.1465                   # <0, AD4 distance-dep.diel;>0, constant
```

Replace BR with any other atom type, i.e. CL and rerun autogrid.

## Prepare a docking parameter file

```bash
/Library/MGLTools/1.5.6/bin/python /Library/MGLTools/1.5.6/MGLToolsPckgs/AutoDockTools/Utilities24/prepare_dpf42.py -l zinc_20031600.pdbqt -r 4iys.pdbqt
```

Which will output `zinc_20031600_4iys.dpf`.

## Run autodock4

`autodock4 -p zinc_20031600_4iys.dpf`

`autodock4 -p zinc_20031600_4iys.dpf  795.51s user 10.21s system 84% cpu 15:55.76 total`

## Results

Within the resulting `.dlg` file the RMSD can be found:

```
	RMSD TABLE
	__________

_____________________________________________________________________
     |      |      |           |         |                 |
Rank | Sub- | Run  | Binding   | Cluster | Reference       | Grep
     | Rank |      | Energy    | RMSD    | RMSD            | Pattern
_____|______|______|___________|_________|_________________|___________
   1      1      1       -6.67      0.00     29.30           RANKING
   2      1     10       -6.15      0.00     28.06           RANKING
   3      1      6       -5.77      0.00     31.35           RANKING
   3      2      5       -5.73      0.10     31.37           RANKING
   4      1      4       -5.61      0.00     28.04           RANKING
   4      2      9       -5.57      0.10     28.09           RANKING
   5      1      3       -5.49      0.00     31.52           RANKING
   6      1      8       -5.47      0.00     31.69           RANKING
   7      1      2       -5.36      0.00     29.75           RANKING
   8      1      7       -5.18      0.00     28.60           RANKING
_______________________________________________________________________
```

The lowest Estimated Free Energy of Binding in kcal/mol is shown in Rank 1 (best pose).


# Docking simulation using AutoDock Vina

Vina docking simulations runs significantly faster than AutoDock

## Prepare configuration file

Note: the sizes for Vina are in Angstrom, not in grid points like in AutoDock. By default, 1 grid point = 0.375 Å, therefore 60 grid points = 22.5Å

```
receptor = 4iys.pdbqt
ligand = zinc_20031600.pdbqt
center_x = -19.951 # Center of Grid points X
center_y = -7.611 # Center of Grid points Y
center_z = -25.596 # Center of Grid points Z
size_x = 22.5 # Number of Grid points in X direction
size_y = 22.5 # Number of Grid points in Y Direction
size_z = 22.5 # Number of Grid points in Z Direction
```

## Run Vina

`autodock_vina_1_1_2_mac/bin/vina --config vina_config.txt`

Can also be run with the config file including only grid information:

```
autodock_vina_1_1_2_mac/bin/vina --receptor 4iys.pdbqt\
--ligand zinc_20031600.pdbqt --config vina_config2.txt
```

# Running Vina on multiple ligands

Convert MOL2 files to PDBQT

```python
import subprocess

files = subprocess.check_output(["ls"]).split('\n')[1:-1]
for line in files:
    pdb_file = "{}.pdb".format(line.split(".")[0])

    # convert MOL2 to PDB using OpenBabel
    subprocess.call(["babel", line, pdb_file])
    
    # prepare PDBQT for the ligands
    subprocess.call(["/Library/MGLTools/1.5.6/bin/python", "/Library/MGLTools/1.5.6/MGLToolsPckgs/AutoDockTools/Utilities24/prepare_ligand4.py", "-l", pdb_file])
```

Run Vina:

```bash
for line in `ls *.pdbqt`; 
do echo $line; ~/autodock_vina_1_1_2_mac/bin/vina\
--receptor ../4iys.pdbqt --ligand $line\
--config vina_config2.txt; 
done
```

Get the lowest energy per ligand:

```python
import subprocess
vina_output = subprocess.check_output("ls *_out.pdbqt", shell=True).split('\n')[:-1]
for vina_file in vina_output:
    top_hit = subprocess.check_output('grep "REMARK VINA RESULT" {}|head -1'.format(vina_file),
                                      shell=True).strip().split("REMARK VINA RESULT:")[1].split()[0]
    print vina_file.split(".")[0].split("_out")[0], '\t', top_hit
```

