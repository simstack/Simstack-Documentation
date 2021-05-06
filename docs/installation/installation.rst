#. Downloading the **SimStack** client

For Linux and Windows systems, the latest version of the **SimStack** client is available `here <https://www.simstack.de/?page_id=216>`_.
The client version installs itself and all dependencies during the first launch. After extracting the ``.tar.gz``
or ``.zip`` files from the downloaded archive just start this process:

.. figure:: /assets/Simstack_client_server.png

   Caption goes here

Windows::

    cd ~
    sudo apt-get update
    sudo apt-get install python3
    sudo apt-get install python3-venv
    python3 -m venv ~/VENV/kmcos
    source ~/VENV/kmcos/bin/activate

To use kmcos after this installation, you will need to use that source activation command from the terminal each time.  When finished, you can exit this virtualenv by typing 'deactivate'. 

Linux setup::

        bash
        cd  simstack_linux
        ./run_simstack.sh

Windows setup::
       
        Double click on `run-simstack.bat`


## Connect to compute ressources (SimStack Server)

### Passwordless SSH

For communicating with a compute backend, the SimStack client requires passwordless SSH access. If you do not have `ssh` access to the HPC resource already preconfigured, or are provided with an SSH key in the context of a tutorial, you need to generate a SSH keypair and transfer it to the Compute backend. This can be achieved with two simple commands:

1. Linux

```
ssh-keygen -t ed25519
ssh-copy-id tutorialXX@int.bionano.int.kit.edu
```

2. Windows (https://phoenixnap.com/kb/generate-ssh-key-windows-10)

### Simstack Server Configuration

Setup the server by opening the configuration menu: `Configuration` -> `Servers`
![simstack_configuration.png](../assets/simstack_configuration.png)

If passwordless `ssh` is setup correctly, you should now be able to connect by clicking the `Connect` button at the top right of SimStack:
![simstack_gui.png](../assets/simstack_gui.png)

