Downloading the **SimStack** client
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For Linux and Windows systems, the latest version of the **SimStack** client is available `here <https://www.simstack.de/?page_id=216>`_.
The client version installs itself and all dependencies during the first launch. The client version installs itself 
and all dependencies during the first launch. After extracting the ``.tar.gz`` or ``.zip`` files 
from the downloaded archive, run the proper commands according to your system.

For communicating with a compute backend, the client version requires passwordless via `ssh` access.
If you do not have  `ssh` access to the HPC resources already preconfigured, you need to generate a
`ssh`keypair and transfer it to the Compute backend. You achieve this with two simple commands, as shown below.

1. Installation on Linux::

   cd  simstack_linux
   ./run_simstack.sh

.. warning:: If you don't have the `ssh` keys, use the steps below to generate them..
        
   * SSH Key generation and copying to the HPC resource:: 
        
        ssh-keygen -t rsa 
 
   * The ssh-key command in the step above generated two keys in the ``~/.ssh`` directory ::  
 
        id_rsa
        id_rsa.pub
        ssh-copy-id tutorialXX@int.bionano.int.kit.edu


1. Installation on Windows::
  
   Double click on ``run-simstack.bat``

   * This `website <https://phoenixnap.com/kb/generate-ssh-key-windows-10>`_ 
     has a clear explanation of how to generate a `ssh` key on Windows 10.

.. warning:: Make sure that the `ssh` is enabled on your Windows system.

.. note:: For this tutorial, the HPC resource considered here is the *bionano* cluster.


.. _Configuration:

Simstack Server Configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Setup the server by opening the configuration menu: ``Configuration`` -> ``Servers``
.. figure:: /assets/simstack_configuration.png

* If `ssh` key is setup correctly, you should now be able to connect by clicking the `Connect` button at the top right of SimStack.
  The green button means you successfully connect to the server. 
.. figure:: /assets/simstack_gui.png

.. warning:: If you get an error message during your try, double-check the field on the server setup.

Simstack Overview
^^^^^^^^^^^^^^^^^


.. figure:: /assets/simstack_overview.png

        **SimStack**'s basic graphical user interface elements.

Using the **SimStack** client (picture above), simulation workflows are constructed by dragging and 
dropping various  (already incorporated modules) from the window on the left side area (**Available WaNos**) into 
the **Workflow canvas area**. Double click each module to modify module-specific parameters (see **input file** field) 
and allocate resources in the **Requested computational resources**  field for each module. To save and reuse your workflow 
lately, press ``` Crtl+S``` or ```File -> Save```. It will then appear in the left panel **Saved Workflows** and can be 
re-loaded by double-clicking. To submit your workflow, connect to the computational resource (the connect button as shown 
in the last figure of **Simstack Server Configuration section**) and click ```Run -> Run``` on the menu bar,  
or ```Crtl + r```. All required input files are uploaded automatically to the HPC resource, and workflow modules may 
run serially or in parallel, depending on if your workflow uses or not some of the **Loop controls** features. As shown in 
the figure above, the **SimStack** client will display a yellow folder while be running. When successfully finished, 
the client will exhibit a green folder, and you will be able to retrieve all the relevant data from your simulations. If the 
simulation presents a computational issue during the execution, **SimStack**  returns a red folder, which we can be 
inspected to fix the problem.
