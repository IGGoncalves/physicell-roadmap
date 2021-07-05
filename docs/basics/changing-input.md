**The first and easiest way to modify the sample projects code is to change some of the model parameters**. As explained in the previous section, all the code that differentiates a sample project from another can be found either in the `config` or the `custom` folder. In this section, we will focus on the configuration file.

**At this point, it is a good idea to open PhysiCell's User Guide** (available in the `documentation` folder of your repository) to better understand what you can do with PhysiCell. Through this section, I will point out some of the chapters as suggested reading. You can start with **chapter 13**.

## The `PhysiCell_settings.xml` file
This is an XML-based file where general simulation parameters are defined. You can think of this file as an input parameter of your model. You do not need to recompile your project if you make changes to this file, as it does not change how the model works, and it only changes the numerical values that define each parameter.

This file can be divided into 4 main categories:
- **General simulation parameters** - here you define the size of the domain, the length of the simulation, what to save in your inputs,...
- **Microenvironment parameters** - here you define the substances that you want to include in your simulation
- **Cell definition parameters** - here you define the cells you want to include in your simulation, based on the standard PhysiCell definitions
- **User parameters** - here you can define custom variables that are not part of the standard PhysiCell workflow  but you will use in your custom functions

### General parameters
This section is fairly easy to understand and work with. 
- The `domain` variables define the size of the domain. You can also define whether the model is 2D or 3D. 
- The `overall` variables define simulation times. For most use cases, you only need to change the `max_time` variable to define the length of the simulations. You can leave the others as they are (more information on this is available below).
- The `parallel` variables define the number of cores to use during code parallelization. For a regular computer, the value should be left as 4. For larger machines, such as the M2BE cluster, this value can be increased.
- The `save` variables allow you to define the results to save and where to save them. You can choose to save cell plots (in SVG) and cell data (in `.mat` files). To know more about the available output formats, **check out chapter 14 of the User Guide**. 
- The `options` variables define additional aspects. For instance, you can define whether the edges of the domain should act as walls, bouncing the cells off when they touch, or if the cells should be left at the edge of the domain.

Variables marked as `legacy` are not used in the newest version of the code.

> <details> <p><b>diffusion_dt</b> is the <b>step size used in the diffusion solver</b>, including the secretion/export and uptake processes. The default value is 0.01 min.</p> <p><b>mechanics_dt</b> is the <b>step size for the cell mechanics solver</b>, including cell motility.  Each cell’s custom function is also evaluated on this time scale. The default value is 0.1 min.</p> <p><b>phenotype_dt</b> is the <b>step size for phenotype processes</b> (e.g., cycle progression, volume changes). The default value is 6 min.</p> <summary><b>Click here to learn more about the time steps in PhysiCell</b></summary></details>

### Microenvironment parameters
Check out the [official tutorial](http://www.mathcancer.org/blog/setting-up-the-physicell-microenvironment-with-xml/). Also, **check chapter 8 of the User Guide**.

### Cell definitions parameters
This is a new addition to the configuration file, so it is not covered in the User Guide yet. There are also a lot of parameters to go through here, so the best option is to read **chapters 9, 10 and 11** of the User Guide, which go through the Cell object in PhysiCell.

Once you are aware of how cells are defined, you can open the configuration file of one of the newest projects (for instance, the worm project) and you should be able to understand how to modify the input value of the cell definition parameters. To learn how to define multiple types of cells, check out the configuration file of the predator_prey_farmer project.

### User parameters
Check out the [official tutorial](http://www.mathcancer.org/blog/user-parameters-in-physicell/). Note that this tutorial also goes through how you can access these variables in your code. If you do not feel comfortable with the code yet, you can disregard this part of the tutorial.

## The `cells.csv` file
This is also a new addition to the PhysiCell workflow. The idea here is to define the coordinates of the initial cells, so that you can test different spatial configurations without having to recompile the code. However, this feature is still in development, so we will disregard this and define the initial coordinates in the `custom.cpp` file.