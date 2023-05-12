===================
Server Installation
===================

.. raw:: html

    <style> .red {color: red !important} </style>
    <style> .green {color: green !important} </style>

.. role:: red
.. role:: green

This manual is verified for SimStackServer v1.3.4

Installing the **SimStack** server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SimStackServer requires a Linux system. If you do not have a working conda or mamba installation, please install mambaforge for your architecture from `github.com/conda-forge/miniforge <https://github.com/conda-forge/miniforge>`_.

After installing, make sure you have the **mamba** command available in your shell and call:

.. code-block:: bash

   # Create a new environment for simstack client:
   mamba create --name=simstack_server_v6 simstackserver -c https://mamba.nanomatch-distribution.de/mamba-repo -c conda-forge
   # Activate the environment to see if it exists
   conda activate simstack_server_v6

Note down the path of your mambaforge install (e.g. */home/you/mambaforge*), you will need to insert this into the client, when configuring.


Example: Setting required WaNo exports
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


Many WaNos require a specific export, such as **NANOMATCH** to find their executables. To set this variable, please call the following with an activated environment:

.. code-block:: bash

   conda activate simstack_server_v6
   conda env config vars set NANOMATCH=/path/to/your/nanomatch/folder
   # To see if it worked:
   conda deactivate
   conda activate simstack_server_v6
   echo $NANOMATCH


Once this is finished, continue with the client setup. If you are testing and do not have a working queueing system installed, choose ``Internal`` as queueing system.
If you are running on a HPC machine, install an appropriate queueing system, e.g. Slurm, and select this in the client.
