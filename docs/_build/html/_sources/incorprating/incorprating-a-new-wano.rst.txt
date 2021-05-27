.. raw:: html

    <style> .green {color:green} </style>

.. role:: green

Scientific studies are often obtained by chaining the preparation and execution of multiple interoperable packages 
one after the other. The scientific process requires the reproducibility of this simulation chain and the reproducibility 
of the singular modules. Here we show how to incorporate a new **WaNo** within in **SimStack** framework, including 
its GUI, parameters, and execution process. 

1. WaNo concept
###############

The Workflow Active Nodes **WaNo** is specified in an ``XML`` file, which **SimStack** interprets and uses to render 
the information of the node from the local machine to the HPC resources. It eases the adjustment of input parameters 
and files and is displayed on the right side of the client window, as shown in the last figure of the **Installation** 
section. In the code lines below, we highlight in yellow the five possible fields. The absence of the first one will 
not raise any execution error, but the remaining are mandatory for any implemented **WaNo**.

.. code-block:: XML
 :emphasize-lines: 2, 13, 15, 18, 20, 22, 24, 26, 28, 30 

 <WaNoTemplate>
    <WaNoMeta>
       <Author>
         <Name> Celso R. C. Rego </Name>
         <Email>celsorego@kit.edu</Email>
       </Author>

       <Description>
         This WaNo performs ...
       </Description>

       <Keyword>Some nice words</Keyword>
    </WaNoMeta>

    <WaNoRoot name="TemplateWaNo">
        Load the input files from a given folder
        Define a set of parameters
    </WaNoRoot>

    <WaNoExecCommand>
        Run the simulation
    </WaNoExecCommand>

    <WaNoInputFiles>
        Name of the mandatory files, e.g., scripts.
    </WaNoInputFiles>

    <WaNoOutputFiles>
        Define the expected output files
    </WaNoOutputFiles>
 </WaNoTemplate>

Every element is required to have a name attribute. This name cannot contain "." characters. Below 
we give an overview of the meaning for each element inside the ``WaNoTemplate`` in the ``XML`` file above.

- ``WaNoMeta`` This field is dedicated to the developer information and describes the aims of the **WaNo**.
- ``WaNoRoot`` Here is where we define the set of parameters to be exposed and the inputs files of the simulation.   
- ``WaNoExecCommand`` This part is a multiline string, which contains the script or program to execute, when the **WaNo** starts. 
- ``WaNoInputFiles`` This segment is where we name all static input files, which have to be present in the **WaNo** folder.
- ``WaNoOutputFiles`` Here is where we name all the expected output files in the output directory. If not 
  present, your **WaNo** will be shown as aborted (red folder).

2. Morse potential example
##########################

In this example, we want to include a python program in our **WaNo**. It computes the `Morse potential<https://en.wikipedia.org/wiki/Morse_potential>`_  :math:`V(r)=D_{e}[1-e^{-a(r-r_{e})}]-D_{e}` 
energy of  a particular diatomic molecule as a function of the intermolecular distance :math:`(r-r_{e})` using  `Numpy <https://numpy.org/>`_. Here 
:green:`De` is the well depth energy relative to the atoms apart from each other. :green:`a` is the controls the width of the potential, 
:math:`\color{green}{r_{e}}` gives the minimum  potential distance. This scrip loads ``.yml`` file from where it reads the inputs to compute 
the Morse energy,  via the command line, this script is executed as follows:

.. code-block:: bash

 python/intepretor morse.py

2.1 Starting a new **WaNo** project
***********************************

To incorporate a new tool, first create a new directory with the **WaNo** name, e.g., *Morse-pot* (see the code lines below) in the 
**WaNo** repository directory, see Paths configuration in **SimStack** **Installation** section. The WaNo name should be unique. In our example, 
we name our new **WaNo** 'MORSE-pot'. :ref:`installation`

.. code-block:: bash

 mkdir Morse-Pot
 cd Morse-pot

Create a `Morse-pot.xml` file, and in this we will specify the GUI elements in this **WaNo**.

To give our new **WaNo** an icon image, we could add an image `MORSE-Pot.png`

directly under the WaNo directory. In such a way, SimStack client would automatically load this image.


2.2 Morse potential ([Wikipedia](https://en.wikipedia.org/wiki/Morse_potential))
*********************************

We think for a while, to what aspect in this simulation project we want to emphasis; which parameters should be fixed, which are adjustable.  For general purpose, we make all Morse potential parameters flexible.

Let's start with the Python script, `morse.py`. It accepts arguments not only to specify the Morse potential shape, but also to specify inter-molecular distance.  And we also want to write the computed result in a file <font color="#cc6600">MOROUT</font>.   For details, please refer to the following.


```python
import sys, os, yaml

def Vmorse(r,De, a, re):
    """Calculate the Morse potential, V(r).
    """
    return De * (1.0 - np.exp(-a*(r - re)))**2.0 - 1.84


if __name__ == '__main__':
    
    with open('rendered_wano.yml') as file:
        wano_file = yaml.full_load(file)

    decimal_points = 6 # decimal points

    De = wano_file["De (Ry)"] #0.48 #Ry
    a =  wano_file["a"] #1.8 
    re = wano_file["re (A)"] #0.8 #Angs
    r = wano_file["Mol_distance (A)"]  #0.4 #Angs
    
    # get morse potential energy
    ymorse = Vmorse(r, De, a, re)

    MOROUT = wano_file  # output file
    
    MOROUT["energy"] = float(round(ymorse,decimal_points))
    try:   
        with open("MOROUT.yml",'w') as out:
            yaml.dump(MOROUT, out,default_flow_style=False)
    except IOError:
        print("I/O error")
```

And we give this script the execution access.

For a lot of computed problems, we could also have binaries direct available in our server machine.   We put this Python script inside WaNoInputFile tag.
```xml
	<WaNoInputFiles>
		<WaNoInputFile logical_filename="morse.py">morse.py</WaNoInputFile>
	</WaNoInputFiles>
```
The logical_filename property would map the input file into
the given file name when transferred to the server side.

We need our output of the script within SimStack management, so we add  
```xml
    <WaNoOutputFiles>
        <WaNoOutputFile>MOROUT.yml</WaNoOutputFile>
    </WaNoOutputFiles>
```
Regarding to the parameters, we need them adjustable within _SimStack_ client. For instance, we need well depth <font color="#cc6600">De</font> ; we can add inside the _WaNoRoot_ tag
```xml
    <WaNoFloat name="De (Ry)" description = "The well depth (defined relative to the dissociated atoms)">0.48</WaNoFloat>
```

This means we put an adjustable parameter with its name as <font color="#cc6600">De</font>, units in Rydberg, and its default value is 0.48.  Within WaNo client, a WaNoFloat UI element would accept float data type. With the same spirit, we set up other two parameters. They are  <font color="#cc6600">a</font> with default value 1.8,  <font color="#cc6600">r<font size=1>e</font> </font> with default value 0.8.

```xml
    <WaNoFloat name="a" description = "Controls the width of the potential (the smaller a is, the larger the well)" >1.8</WaNoFloat>
    <WaNoFloat name="re (A)" description = "The equilibrium bond distance">0.8</WaNoFloat>
```

These three parameters basically set up the shape of the Morse potential. Finally we add the distance where we want to compute the potential inside WaNoRoot.
```xml
    <WaNoFloat name="Mol_distance (A)" description = "Distance between the atoms" >1.0</WaNoFloat>
```

Every parameter comes with its description. The WaNo shall be as the following figure. It is ready to use.

<img src="../assets/wano_edit.png"  width="100%">


## 3. Tips and tricks

- If we start a new **WaNo** for the first time, download a **WaNo**, copy this **WaNo** into local **WaNo** repository and modify it. This makes a quick start.

- A lot of scientific packages have a variety of parameters that could, in principle, all be set by the end user. However, for specific, reoccurring user cases, only a specific subset of parameters need be set in one project.   

- When we start a new **WaNo**, we need clarify what parameters we need to vary in this specific project, and only include those into WaNo and fix the rest in the scripts.   

- Depending on the tool/case, it may be beneficial to provide several separate **WaNos** for one program.Adaptions to the **WaNo** to allow more flexibility is a matter of minutes.
