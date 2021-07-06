When you need your model to go further than changing the numerical values of your input parameters, **it's time to make some changes to the custom functions that define how the model behaves**. This is done in the `custom.cpp` and `custom.h` files.

I believe the best way to understand how to design a model using custom functions is to use the sample projects as examples. Most of them rely on custom functions that are part of the PhysiCell code, found in the `PhysiCell_standard_models.cpp` inside the `core` folder. Make sure to check **chapters 17 and 19** of the User Guide, as well as the **original publication**, which goes through each sample project in more detail. **Chapter 21** is also important to understand the functions that define the cell cycle.

Thus, in this section I will mainly focus on the main aspects of building a custom model.

## The `custom.cpp` file
Let's analyze the `custom.cpp` file that defines the `template` sample project. This is the most basic of all the sample projects, so it has the simplest structure. Other projects will build up on this code.

### Create cell types

```cpp
void create_cell_types( void );
```

This function creates **cell definitions** and can be divided in two main parts. Firstly, it defines the **functions common to all cell types**, and then it defines **functions specific to each cell type**. It also uses the information found in the XML file to define each cell type.

### Microenvironment
```cpp
void setup_microenvironment( void );
```

The next function in the file will **initialize the microenvirnoment, using the information found in the XML file.**

In case you want a substance to have a **non-uniform initial distribution**, you can extend this function to go through the domain and change the value of that substance to a new value. For instance, if we wanted to define an **initial concentration of glucose ranging from 0 to 1** we could write the following function instead.

```cpp
void setup_microenvironment( void )
{
	// set domain parameters 
	
	// put any custom code to set non-homogeneous initial conditions or 
	// extra Dirichlet nodes here. 
    // Glucose initial condition
	// set a new initial condition for glucose
	int glucose_index = microenvironment.find_density_index( "glucose" ); // find its index
	// go through all the voxels in the domain
	for( int voxel_index=0; voxel_index < microenvironment.number_of_voxels(); voxel_index++ )
	{
		microenvironment(voxel_index)[glucose_index] = UniformRandom();
    }
	
	// initialize BioFVM 
	
	initialize_microenvironment(); 	
	
	return; 
}
```

Note that `UniformRandom()` is a function defined by PhysiCell that returns a random value between 0 and 1. You can find its defintion in `PhysiCell_utilities.cpp`, alongside other functions to simulate random events.

### Tissue setup
```cpp
void setup_tissue( void );
```

Here you define the **cells' initial coordinates**, and you create the cell objects, placing them in the defined location. You can check the `PhysiCell_geometry.cpp` file, found inside the `modules` folder, for some functions that place cells in a given geometry (i.g., a circle, a rectangle,...).

Alternatively, it can load the coordinates found in the `cells.csv` file.

### Other custom functions
Finally, there are three custom functions:

- `phenotype_function` defines changes in the cell phenotype. For instance, you could define a function that would increase apoptosis rates when oxygen levels are low. Check **section 19.1.4** of the User Guide for an example.
- `contact_function`  defines a contact force between two neighbor cells. For instance, you could define an elastic or viscoelastic force.
- `custom_function` defines changes in the cell behavior, and it is not specific to a cell function.

By default, these cells are left as blank.

## Standard custom function
For some examples of custom functions that are already part of the PhysiCell code, check **chapter 19 of the User Guide** as well as the `PhysiCell_standard_models.cpp` file found in the `core` folder.

