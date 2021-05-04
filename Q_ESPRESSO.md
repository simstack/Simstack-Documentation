## Project: Q_ESPRESSO

This workflow performs several DFT calculation, using the Quantum ESPRESSO code,
 to generate energy as a function of the intermolecular distance between two Hydrogen atoms. 
 To generate this workflow, we combine three WaNos. 
 The WaNo (Iterator) is responsible for passing the interatomic distance for two Hydrogen atoms. 
 The second WaNo (Q_ESPRESSO) will perform a single shot DFT calculation for a given nuclear configuration. 

In this project, we aim to show you how the Simstack submits __*High-Throughput Calculations*__ can be combined. 
To run this example, follow the steps below.    

### <font color="green">Step 1</font>
 Open Simstack on your computer and connect to your remote resource.
### <font color="green">Step 2</font>
 Drag and drop the ForEach loop control from the bottom left menu to the empty area.
### <font color="green">Step 3</font>
Drag and drop the Iterator Wano from the top left menu to the top of the ForEach loop.
If the WaNo order is incorrect after the first drag&drop, you can change the WaNo Order by drag and drop.
### <font color="green">Step 4</font>
 Drag and drop the Q_ESPRESSO Wano from the top left menu to the center of the ForEach loop.
### <font color="green">Step 5</font>
 A double click on the WaNo (Q_ESPRESSO) will allow you to change the Input parameters.
The figure below, explains the mentioned steps in more detail.

<img src="../assets/WaNo_Q_ESPRESSO.png"  width="600" height="500">

#### <font color="green">Inputs parameters</font>
Changes to the parameters below (see figure below) are automatically passed to the Quantum Espresso code input file.

    - Calculation
    - Lattice Constant (A)
    - Ecut (Ry)
    - Element
    - Mol_distance (A)
    - QEIN.in (path to the input file)

<img src="../assets/Only_WaNo_Q_ESPRESSO.png"  width="600" height="500">

#### <font color="green">Input file </font>
    * QEIN.in

#### <font color="green">Output file</font>

In each folder a file, named QEOUT, will be generated after the end of the calculations. This file contains the input parameters as well as all Quantum ESPRESSO output information.

### Congratulations! You have performed your first __*High-Throughput Calculations*__ in the Simstack framework.
