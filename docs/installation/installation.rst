Downloading the **SimStack** client
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For Linux and Windows systems, the latest version of the **SimStack** client is available `here <https://www.simstack.de/?page_id=216>`_.
The client version installs itself and all dependencies during the first launch. The client version installs itself 
and all dependencies during the first launch. After extracting the ``.tar.gz`` or ``.zip`` files 
from the downloaded archive, run the proper commands according to your system.

For communicating with a compute backend,  the client version requires passwordless via `ssh` access. If 
you do not have  `ssh` access to the HPC resources already preconfigured,  you need to generate a `ssh` 
keypair and transfer it to the Compute backend. You achieve this with two simple commands, as shown below. 

1. Installation on Linux::

        cd  simstack_linux
        ./run_simstack.sh

 * SSH Key generation and copying to the HPC resource::
    
        ssh-keygen -t rsa 

 * The ssh-key command in the step above generated two keys in the ``~/.ssh`` directory
   ::     
        id_rsa
        id_rsa.pub
        ssh-copy-id tutorialXX@int.bionano.int.kit.edu


2. Installation on Windows::
  
   Double click on ``run-simstack.bat``

   * This `website <https://phoenixnap.com/kb/generate-ssh-key-windows-10>`_ 
     has a clear explanation of how to generate a `ssh` key on Windows 10.

 .. warning:: Make sure that the `ssh` is enabled on your Windows system.

.. note:: For this tutorial, the HPC resource considered here is the *bionano* cluster.


Simstack Server Configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Setup the server by opening the configuration menu: ``Configuration`` -> ``Servers``
.. figure:: /assets/simstack_configuration.png

* If `ssh` key is setup correctly, you should now be able to connect by clicking the `Connect` button at the top right of SimStack.
  The green button means you successfully connect to the server. 
.. figure:: /assets/simstack_gui.png

.. warning:: If you get an error message during your try, double-check the field on the server setup.

Simstack Overview
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
