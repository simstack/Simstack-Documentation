===================
Client Installation
===================

.. raw:: html

    <style> .red {color: red !important} </style>
    <style> .green {color: green !important} </style>

.. role:: red
.. role:: green


Downloading the **SimStack** client
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For Linux and Windows systems, the latest version of the **SimStack** client is available `here <https://www.simstack.de/?page_id=216>`_.
The client version installs itself and all dependencies during the first launch. After extracting the ``.tar.gz`` or ``.zip`` files
from the downloaded archive, move it to your **local filesystem**, and run the proper commands according to your operating system.

The client version requires passwordless via ``ssh`` access to communicate with the HPC. If you do not have passwordless via
``ssh`` access to the HPC resources already preconfigured, you need to generate a ``ssh`` keypair and transfer it to your
``authorized_keys`` file of your user account on the available HPC resource. You achieve this with two simple commands,
as shown below.

.. warning:: Please run the below commands on the same local machine, where the **SimStack** client will be installed.

Installation on Linux
^^^^^^^^^^^^^^^^^^^^^

If you don't have the ``ssh`` keys, use the steps below to generate them.

   * ``ssh`` key generation, just press enter for the passphrase option.

      .. code-block:: bash

         ssh-keygen -t rsa

   * The ssh-key command above generated two keys in the ``~/.ssh`` directory.
     Now you have to copy the key to your user account in one of the available HPC resources.

      .. code-block:: bash

        id_rsa
        id_rsa.pub

   * Please choose the HPC where you want to have passwordless access.

      .. code-block:: bash

         ssh-copy-id user@int.bionano.int.kit.edu
         ssh-copy-id user@int-nano.int.kit.edu

   * Test the connectivity of your passwordless ``ssh``  by running one of the commands below in the **Powershell** prompt.

      .. code-block:: bash

         ssh user@int-nano.int.kit.edu
         ssh user@int.bionano.int.kit.edu

   * After completing, the above steps runs the below commands.

      .. code-block:: bash

         cd  simstack_linux
         ./run_simstack.sh


Installation on Windows
^^^^^^^^^^^^^^^^^^^^^^^


If you don't have the ``ssh`` keys, use the steps below to generate them.

   * Make sure that the `ssh` is enabled on your Windows system.

   * Check if **Powershell** is installed on your Windows system, if not you can install it from the Microsoft Store.

   * To generate a public/private ``rsa key pair`` on Windows, open the **Powershell** prompt run the
     below command, and just press enter for the passphrase option.

     .. code-block:: bash

         ssh-keygen

   * To copy the ``ssh`` key to your user account on the HPC resource, choose and run
     one of the commands below in the **Powershell** prompt. :green:`Literally copy the command changing only the` **user**.

      .. code:: bash

         type $env:USERPROFILE\.ssh\id_rsa.pub | ssh user@int-nano.int.kit.edu "cat >> .ssh/authorized_keys"
         type $env:USERPROFILE\.ssh\id_rsa.pub | ssh user@int.bionano.int.kit.edu "cat >> .ssh/authorized_keys"


   * After completing, the above steps, double click on ``run-simstack`` and be happy.

**Testing the connectivity**

You can test the connectivity of your passwordless ``ssh`` in both systems by running one of the
commands below. You successfully transferred the key if you establish the ``ssh`` connectivity to
your HPC without entering your user password.

   .. code-block:: bash

      ssh user@int-nano.int.kit.edu
      ssh user@int.bionano.int.kit.edu

.. warning:: The HPC resource considered here for this tutorial are the *int-nano* (first line) and *bionano*
      (second line) clusters. Please note that you must replace the ``user`` with your user account characters
      in the above lines, and here we are considering that you named your public ``ssh`` key as ``id_rsa.pub``
      located in the ``.ssh\`` directory. This `website <https://www.chrisjhart.com/Windows-10-ssh-copy-id/>`_
      has a detailed explanation of how to generate ``ssh`` keys on Windows and copy it to your HPC resource.

.. _Configuration:

Simstack Server Configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Setup the server by opening the configuration menu: ``Configuration`` -> ``Servers``

.. figure:: /assets/simstack_configuration.png

You must replace the characters ``xxxxxx`` with your proper setup as highlighted in the figure above,
and don't forget to load (**SSH Private Key**) your ``ssh`` key.

   - **Registry Name**: accepts any name.

   - **Base URI**: can accepts any HPC IP, but here we will limit ourselves with one of the below options.

       - int-bionano.int.kit.edu
       - int-nano.int.kit.edu

   - **Username**: enter with the user account according to your available HPC resource.


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
