Although running replicates may be useful, sometimes you may also want to **run your project, make slight changes to the code, and then run it again**, with these new conditions. This is particularly helpful in **parameter studies**.

Instead of making these changes manually, you can automate this action by building a **script that modifies the XML PhysiCell configuration file** according to the parameters you want to vary.

As an example, let's assume we want to run a study with **two different collagen concentrations.** Using **Python**, we can create a simple script (change_settings.py) that:

  - Receives the value we want the collagen concentration parameter to assume;
  - Opens the XML file;
  - Writes this value and saves the file.

```python
import sys                                  # To read the terminal inputs
from xml.etree import ElementTree as et     # To change the XML file

# Variable definition
folder_name = 'config/'
file_name = "PhysiCell_settings.xml"
modified_element = "microenvironment_setup/variable[@name='ECM']/initial_condition"

# Read and update file
tree = et.parse(folder_name + file_name)
tree.find(modified_element).text = str(sys.argv[1])
tree.write(folder_name + file_name)
```

Then, we can adapt our previously developed bash script

```bash
#!/bin/bash

# Create results folder
folderName='results'
mkdir $folderName

# Define density values [mg/mL]
densityValues=[4, 6]

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

Of course, you can modify our Python file to adapt to any of the possible parameters, by changing the `#!python modified_element`. Or, even better, you can extend the script to receive two arguments: the parameter to be changed and its corresponding value. Maybe even two lists... The possibilities are endless! 