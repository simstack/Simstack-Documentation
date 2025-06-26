===================
Server Installation
===================

.. raw:: html

    <style> .red {color: red !important} </style>
    <style> .green {color: green !important} </style>

.. role:: red
.. role:: green

This manual is verified for SimStackServer v1.3.9

Installing the **SimStack** server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SimStackServer requires a Linux system with a micromamba or conda install. You can use your existing micromamba or conda installation to install SimStackServer. If you do not have a working micromamba for your architecture please install micromamba, e.g. via the automatic installation route `micromamba install docs <https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html>`_. Note down the path of your `MAMBA_ROOT_PREFIX`, which is set during install. You will need to insert this into the client, when configuring.

After installing, make sure you have the **micromamba** command available in your shell and call:

.. code-block:: bash

   # Create a new environment for simstack client:
   micromamba create --name=simstack_server_v6 simstackserver https://repo.prefix.dev/simstack simstackserver -c conda-forge
   # Activate the environment to see if it exists
   micromamba activate simstack_server_v6

If you want to use a full conda install (not recommended, but supported) instead, make sure your conda is updated and substitute conda with micromamba. The path you have to input in your client is the path of your conda install then.


Example: Setting required WaNo exports
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Note: The next section does not apply for the newest WaNos by Nanomatch.
Some WaNos require a specific export, such as **NANOMATCH** or **KIT** to find their executables. To set this variable, please call the following with an activated environment:

.. code-block:: bash

   micromamba activate simstack_server_v6
   micromamba env config vars set NANOMATCH=/path/to/your/nanomatch/folder
   # To see if it worked:
   micromamba deactivate
   micromamba activate simstack_server_v6
   micromamba $NANOMATCH


Once this is finished, continue with the client setup. If you are testing and do not have a working queueing system installed, choose ``Internal`` as queueing system.
If you are running on a HPC machine, install an appropriate queueing system, e.g. Slurm, and select this in the client.
