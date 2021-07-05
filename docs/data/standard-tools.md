There are many options when it comes to analyzing your PhysiCell results. Mainly, there are two categories: tools for data **processing** and for data **visualization**. However, some of the presented frameworks can be used to achieve both types of analysis.

There is no definite answer to the questions "Which tool is the best?" or "What framework should I use?", as this depends on what you are trying to achieve, as well as your previous knowledge and experience with the available tools. Thus, here we'll go through some of the options to illustrate their potential, and make this choice a bit easier.

## Data analysis (and some visualization)

When it comes to processing data, both **Python** and **MATLAB** can be used. Currently, my focus is placed on Python, as this is an open-source language and is more accessible to general users. However, if you feel more comfortable with MATLAB, you can choose to do so and adapt some of our Python functions, or implement new features.

### Python

PhysiCell developers have introduced tool, called [python-loader](http://physicell.org/physicell-tools-python-loader/), that allows you to load the data from an output file into a Python object, called **pyMCDS**. Despite being quite **good for exploratory data analysis**, as all outputs are stored in the pyMCDS data structure, this also makes pyMCDS a bit **too slow for processing large amounts of data**. Hence, we have built some custom functions for specific routines, that scale much better. For more information, check the section on [PhysiPy](data-analysis/physipy).

### MATLAB

Just like the **python-loader** module, there are also scripts built by the PhysiCell developers that allow you to **load data into MATLAB**. These can be found [here](http://www.mathcancer.org/blog/working-with-physicell-snapshots-in-matlab/), alongside a tutorial that demonstrates how the data can be processed and visualized once it has been loaded.

## Data Visualization

### ParaView

![paraview](uploads/948f03618f3696018114e9f0e35ab9d5/paraview.png)

ParaView is a great tool to use when you want to look into your cell data to understand what it looks like. Using PhysiCell's [ParaView routines](http://www.mathcancer.org/blog/paraview-for-physicell-part-1/), you will be able to load the data from an output file and automatically render it to a 3D object that can be interacted with. Nevertheless, this tutorial has some mistakes! 

Here are some of the issues I have found:


### POVWriter
[![povray](https://img.youtube.com/vi/nJ2urSm4ilU/0.jpg)](https://www.youtube.com/watch?v=nJ2urSm4ilU)

POVWriter is not as flexible as ParaView, as it renders data into a static image and not an interactable object. However, it offers high-quality renderings of your results. Plus, it can be programmed to adapt to your own style and you can use some simple additional tools to create animations. Check [PhysiCell's tutorial](http://www.mathcancer.org/blog/povwriter/) for more information on how to use this tool.
