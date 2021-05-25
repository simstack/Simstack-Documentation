## Incorporating a new WaNo

Scientific studies are often obtained by chaining the preparation and execution of multiple interoperable packages one after the other. The scientific process requires the reproducibility of this simulation chain, but also the reproducibility of singular modules. In this tutorial we design a single simulation module (here called **WaNo**), which includes its GUI, parameters and execution process.

<img src="../assets/structrue.png"  width="100%">

## 1. WaNo concept
The WaNo is specified in an XML file, which is interpreted by SimStack. The SimStack Client uses a WaNo to render, it eases the adjustment of input parameters and files, and is displayed in the right side of the client window. To start copy and paste the following nearly empty template WaNo file, or a WaNo file from another module and open it in a text editor.
```
<WaNoTemplate>
    <WaNoRoot name="TemplateWaNo">
        <WaNoFile logical_filename="input.dat" name="datafile">Provide an input.dat file</WaNoFile>
        <WaNoDropDown name="Calculate Partial Charges">
            <Entry id="0" chosen="True">Yes</Entry>
            <Entry id="1">No</Entry>
            <Entry id="2">Maybe</Entry>
        </WaNoDropDown>
        <WaNoBool name="Example Bool">False</WaNoBool>
        <WaNoFloat name="Temperature">10.0</WaNoFloat>
    </WaNoRoot>
    <WaNoExecCommand>#!/bin/bash
cat input.dat
echo "It is {{ wano["Temperature"] }} degrees outside."
    </WaNoExecCommand>
    <WaNoInputFiles>
       <WaNoInputFile logical_filename="static_file.dat">static_file_input.dat</WaNoInputFile>
    </WaNoInputFiles>
    <WaNoOutputFiles>
    </WaNoOutputFiles>
</WaNoTemplate>
```

When dragging and dropping this WaNo into the SimStack program, the following UI will be rendered:

![ ](assets/writing_wano.png "Template WaNo")

UI elements and therefore simulation parameters are set inside the WaNoRoot tag. We have used as an example:
- _WaNoFile_ A file element to upload a local file or pass a workflow file
- _WaNoDropDown_ A multiple choice dropdown element resolving to a string
- _WaNoBool_ A True/False boolean checkbox
- _WaNoFloat_ A floating point number.

Every element is required to have a name attribute. This name cannot contain "." characters. <br/><br/>

The other elements inside the WaNoTemplate root tag are: 
- _WaNoExecCommand_ A multiline string, which contains the script or program to execute, when the WaNo starts
- _WaNoInputFiles_ Static input files, which have to be present in the WaNo directory
- _WaNoOutputFiles_ Output files, which are expected in the output directory. If not present, your WaNo will be shown as aborted.

The execution command already shows, how to access WaNo variables. In this case standard jinja2 syntax is employed. All WaNo variables are present in the wano variable. For example wano["Temperature"] resolves to 10.0 in our example.

 ## 2.  Example
In this example,  we want to include a python program in our WaNo. It computes a Morse Potential value at a certain intermolecular distance using  [numpy](https://numpy.org/). Via the command line, the script is executed as follows:
```bash
    ./correct/python/intepretor morse.py [args]
```

Here we can specify well depth <font color="#cc6600">De</font> ,   parameter  <font color="#cc6600">a </font> controls the width of the potential, <font color="#cc6600">r<font size=1>e</font> </font> gives the minimum potential distance.  It is usually a good practice to execute programs using a shell script in order to set environment variables.


### 2.1 Starting a new **WaNo** project

To incorporate a new tool, first create a new directory with the WaNo name in the WaNo repository directory ( see Setup) in SimStack client; or alternatively, we could create it elsewhere, and copy it to the repository.  The WaNo name should be unique. In our example, we name our new **WaNo** 'MORSE-pot'.
```
    mkdir MORSE_Pot
    cd MORSE_Pot
```

 Create a `MORSE-Pot.xml` file, and in this we will specify the GUI elements in this **WaNo**.

 To give our new **WaNo** an icon image, we could add an image `MORSE-Pot.png`

directly under the WaNo directory. In such a way, SimStack client would automatically load this image.


### 2.2 Morse potential ([Wikipedia](https://en.wikipedia.org/wiki/Morse_potential))

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
