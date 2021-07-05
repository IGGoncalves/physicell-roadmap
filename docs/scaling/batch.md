By now, you should be able to run some simulations on your local machine. However, once you feel comfortable with your model and with the PhysiCell workflow, you may feel the need to automate some parts of the process, so that you can **worry less about running the simulations and start focusing more on understanding the results**.

For instance, you will probably need to **run multiple replicates** in order to test the model and guarantee that the **results are consistent**. Of course, this can be done **manually**, by running the simulation, saving the output results to another folder, and repeating this process as many times as necessary to get the number of replicates you need. However, it is much more efficient to **automate this process**.

> **Consider the following sections as suggestions.** You can follow this structure to get the basic ideas, but you may adapt them to your own workflow. i.g., here we will start with compiled code, but you may want to start your batching process by compiling your code, and that is also a valid option. Feel free to experiment with the code to optimize your routines!

## Basic project structure
Before running the simulations, you should prepare the structure of your project:

  - First of all, you must assure that your PhysiCell is **already compiled**
  - Secondly, you must **create a new folder**, in which you will **place your PhysiCell folder**

So, starting with a folder called "physicell-batch", its structure should look like this:

```
physicell-batch
|- PhysiCell/
  |- *Your PhysiCell code*
```

## Running replicates
If you are aiming to simply **run a number of replicates, all of which share the same initial conditions**, a simple **shell script** can be used. This will tell your machine what to do, and will be placed in our main folder.

Let's create it and call it runReplicates.sh. Now the structure should look like this:

```
physicell-batch
|- PhysiCell/
  |- *Your PhysiCell code*
|- runReplicates.sh
```

Now, in order to build our routine, we know that we will want to **run our executable** (let's assume we are running project3D.exe) and then **move the output files elsewhere**, so that they are not overwritten in the next iteration. Thus, we can start our bash file by creating this folder, using `#!sh mkdir`. We will keep it in our main directory.

```bash
#!/bin/bash

# Create results folder
folderName='results'
mkdir $folderName
```

Now, we can **move to the PhysiCell folder** (using `#!sh cd`) and **start looping** between running simulations and saving the results. We can use a `#!sh for` loop to do so, and, for this example, we will assume we are **running 3 replicates.**

To save the results, we will **create a specific subfolder** in the folder we create at the start of the script, indicating the **replicate ID**. Subsequently, we will **copy the output files to this directory** (`#!sh cp -r`, to copy files recursively). Finally, we can **clean the output folder** (`#!sh make data-cleanup`) to avoid getting mixed data, in case something fails.

Translating this into code, we get:

```bash
cd PhysiCell

# Loop through 3 replicates
for i in $(seq 3) # (Generates a sequence from 1 to 3)
do
  # Run simulation
  ./project3D

  # Create specific folder for the results
  mkdir ../$folderName/output$i
  # Copy results from output to new folder
  cp -r output/. ../$folderName/output$i

  # Empty output folder
  make data-cleanup
done
```

And, it's done! 🥳 Now you can run your runReplicates.sh script and your project will now look something like this, with all your replicates results.

```
physicell-batch
|- PhysiCell/
  |- *Your PhysiCell code*
|- results/
  |- output1/
    |- *Results from simulation 1*
  |- output2/  
  |- output3/  
|- runReplicates.sh
```