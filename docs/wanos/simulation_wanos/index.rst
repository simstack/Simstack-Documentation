=================
Simulation WaNos
=================

.. raw:: html

    <style> .green {color:green} </style>

.. role:: green

* DFT-VASP (:download:`github <https://github.com/KIT-Workflows/DFT-VASP>`) 

.. figure:: /assets/DFT-VASP.png

  The user-friendly DFT-VASP **WaNo** tool! With this tool, you can easily perform Density Functional Theory calculations 
  using the widely-used VASP code without needing extensive knowledge of VASP's functionalities and specifications. The 
  tool offers a variety of methods and only requires the POSCAR file as mandatory input, with all other VASP input 
  files generated or loaded automatically. The common outputs include the OUTCAR, CONTCAR, CHGCAR, and POTCAR files 
  and a lightweight, human-readable database in the `yml` extension, named vasp_results containing key information 
  about the simulation. Have fun!

* DFT-QE (:download:`github <https://github.com/KIT-Workflows/DFT-QE>`)

.. figure:: /assets/dft_qe.png

  Let's start exploring your materials' properties with ease and precision! Welcome to the DFT-QE **WaNo**, which 
  performs DFT calculations using the powerful and flexible Quantum Espresso code! Quantum Espresso is an 
  open-source software package that can handle many systems, from small molecules to extended solids. It provides 
  a wide range of exchange-correlation functionals. It can be used to perform various types of calculations, including 
  ground state properties, electronic structure, and phonon calculations. With our **WaNo**, the pseudopotentials `[SSSP Efficiency (version 1.1.2)] <https://www.materialscloud.org/discover/sssp/table/efficiency>`_
  are automatically identified based on the chemical species specification. All input files are generated or loaded automatically 
  after reading the geometry file in `.cif` format, making it easy for you to start.
