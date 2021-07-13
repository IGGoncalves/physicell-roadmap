Although running replicates may be useful, sometimes you may also want to **run your project, make changes to the input parameters, and then run it again**. This is particularly helpful in **parameter studies**.

## Modifying the XML file wih a script
Instead of making these changes manually, you can automate this action by building a **script that modifies the XML PhysiCell configuration file** according to the parameters you want to vary.

As an example, let's assume we want to run a study with **two different collagen concentrations.** Using **Python**, we can create a simple script, `change_settings.py` that:

  - Receives the value we want the collagen concentration parameter to assume;
  - Opens the XML file;
  - Writes this value and saves the file.

```python
import sys                                  # To read the terminal inputs
from xml.etree import ElementTree as et     # To change the XML file

# Variable definition
folder_name = "config/"
file_name = "PhysiCell_settings.xml"
substance_node = "microenvironment_setup/variable[@name='collagen']
attribute_to_modify = substance_node + "/initial_condition"

# Read and update file
tree = et.parse(folder_name + file_name)
tree.find(attribute_to_modify).text = str(sys.argv[1])
tree.write(folder_name + file_name)
```

Of course, you can modify our Python file to adapt to any of the possible parameters.

## Integration with a bash file

Given that we already have a shell script to run multiple simulations, we can integrate the new Python script in our workflow.

```sh
#!/bin/bash

# Create results folder
folderName='results'
mkdir $folderName

# Define density values [mg/mL]
densityValues=[4.0, 6.0]

cd PhysiCell

# Loop through densities
for d in $(seq 3)
do
  # Change XML with Python
  python change_settings.py $densityValues[d]

  # Run simulation
  ./project3D

  # Create specific folder for the results
  mkdir ../$folderName/density_$i
  # Copy results from output to new folder
  cp -r output/. ../$folderName/density_$i

  # Empty output folder
  make data-cleanup
done
```