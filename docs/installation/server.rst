===================
Server Installation
===================

.. raw:: html

    <style> .red {color: red !important} </style>
    <style> .green {color: green !important} </style>

.. role:: red
.. role:: green


Installing the **SimStack** server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SimStackServer requires a Linux system and will automatically download a MiniForge installation on first execution. Installation does not require admin 
rights on the server machine and can be on the same machine as the one running the client.
Download the archive called ``DATE-simstack-server-environment.tar.gz`` and transfer
them to the HPC machine.

Choose a folder and extract the file:
  .. code-block:: bash

     tar xpf *-simstack-server-environment.tar.gz     
     realpath nanomatch/

Note down the path of the final realpath command. You will need to insert this into the client, when configuring.
   *  If you want to use the embedded MiniForge interpreter (recommended), enter the ``Nanomatch/V6`` directory and execute the file ``postinstall.sh``.
   *  If you want to use your own MiniForge interpreter, make sure ``conda`` and ``mamba`` are in your path and run

      .. code-block:: bash

         cd nanomatch/V6
         mamba env create -f simstack_server_environment.yml

      This will create a new environment called simstack_server_v6 in your MiniForge install.
      Afterwards generate a file called ``nanomatch/V6/simstack_conda_userenv.sh``
      with the following contents:

      .. code-block:: bash

         # Change the path in the next folder to your anaconda installation.
         source /path/to/your/anaconda/etc/profile.d/conda.sh

Once this is finished, continue with the client setup. If you are testing and do not have a working queueing system installed, choose ``Internal`` as queueing system.
If you are running on a HPC machine, install an appropriate queueing system, e.g. Slurm, and select this in the client.
