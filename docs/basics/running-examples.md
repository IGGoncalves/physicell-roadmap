Now that you have download the code, you can see that are a lot of folders and files to look at. 
Before simulating anything, though, you will need to assure that your computer is ready to build the simulations.

## Setting up your local machine
Check out the available tutorials for setting up your system on [Windows](http://www.mathcancer.org/blog/setting-up-a-64-bit-gcc-environment-on-windows/) and [MacOS](http://www.mathcancer.org/blog/setting-up-gcc-openmp-on-osx-homebrew-edition/).

## Running your first simulation
I suggest that you read the `Quickstart.pdf` file, which is located in the main folder. This is the best way to learn what you need to do in order to run simulations on your computer, and also to build and run your first simulation. Try following this guide to run any (or all) of the provided examples. 

Do not focus on the "Visualizing Output" section for now. It shows that there are multiple tools that you can use to look into the data. You do not need to use them all, though! You should think about your problem and what variables you want to analyze, and choose the framework that works best for that use case. We'll discuss this later in the [data analysis section](data-analysis-and-visualization) of the wiki.

For now, you can visualize your results using the first method mentioned in the Quickstart guide: the SVG plots drawn by PhysiCell. This is not a perfect tool, as it does not capture the 3D nature of the models, but it is good enough for a start.

**Keep in mind that a common PhysiCell project only requires you to work directly with two groups of files: the configuration file found in the `config` folder and the `custom.cpp` and `custom.h` files found in the `custom` folder**. These files are what make your model different from any other PhysiCell model and allow you to define how your model should behave. The rest of the code defines functions that allow your model to run, but are not specific.

Of course, you can take a look into the code found in the other folders in order to understand the framework, but it can be overwhelming to do so right after downloading a code. I only recommend it after you are comfortable with a simple model. For a brief description of the code structure, you can check out **chapter 5 of the PhysiCell User Guide** (available in the `documentation` folder of your repository).

## Understanding the makefile rules
Following the `Quickstart` guide, you will be able to run some simulations that have been created and coded previously. All of these projects rely on the core PhysiCell code, but each of them may use different standard functions, and it is even possible that they include new functions, that are not part of PhysiCell's core code.

Looking at the `Makefile` file, in which all the makefile rules are defined, we conclude that all of the `make` rules for the projects follow a similar structure. Namely, they copy the files found in the folder that corresponds to the chosen project and place them in the main folder. For instance, let's consider the rule for the template3D project.

```bash
template3D: 	
	cp ./sample_projects/template3D/custom_modules/* ./custom_modules/
	touch main.cpp && cp main.cpp main-backup.cpp
	cp ./sample_projects/template3D/main-3D.cpp ./main.cpp 
	cp Makefile Makefile-backup
	cp ./sample_projects/template3D/Makefile .
	cp ./config/PhysiCell_settings.xml ./config/PhysiCell_settings-backup.xml 
	cp ./sample_projects/template3D/config/* ./config/
```

Here, the program is copying the following files:

- **Configuration files** - these files define model input parameters.
- **Custom files** - these define custom functions that are specific to the project.
- **Build files** - these files define how the model should run and be built.

Once these files have been copied, the main directory is ready for us to build and run the model. Now, the command `make` can be called, which will build the project and create an executable file with which we can run the model.

Thus, **we should not make changes to the code in the `sample_projects` folder**. These are the templates of our simulations and, once we change them, they will not behave in the same way as described in the PhysiCell guides. All changes should be made to the code found in the main directory, inside the `config` and `custom` folders. We will learn how to do this in the next section.