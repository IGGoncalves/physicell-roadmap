# Programming review

PhysiCell is a very complete piece of software, and you can most likely find some code similar to what you will need in one of PhysiCell's projects. However, it is a good idea to review some basic concepts before starting to dive deep into this framework.

## Basic command line commands
**PhysiCell runs in the command line**, so you will need to know at least some basic commands in order to run your simulations. For a brief introduction on this topic, you can read [this tutorial](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview), or [this one](http://linuxcommand.org/lc3_learning_the_shell.php).

In general, these are the commands you will use the most and that are worth remembering.

```sh
# List the files in the current directory
ls

# Go into a specified folder
cd folder-you-want-to-move-to
# Go back to the previous folder
cd .. 

# Remove file
rm file-you-want-to-remove
# Remove folders 
rm -r folder-you-want-to-remove

# Move file
mv file new-file-location
# Move file into the current directory
mv file .

# Copy file 
cp file new-file-name
```

You may also want to check out this [shell scripting tutorial](https://www.shellscript.sh/first.html).


## C++
C++ is at the core of developing PhysiCell models. **If you are at least somewhat familiar with the language, you will be able to understand PhysiCell's high-level code**, as you can learn from the provided examples. However, as you dig deeper into the code and attempt to modify functionalities at its core, more knowledge about C++ may be required. In addition, PhysiCell's low-level code relies on a parallelization library known as [OpenMP](https://www.openmp.org/). Knowing how to use this library is not essential for most of the use cases, though.

On the other hand, **if you have no previous knowledge of C++**, you may need to study some references such as [CPlusPlus.com](http://www.cplusplus.com/) or [learncpp.com](https://www.learncpp.com/). Both these references are also recommended by PhysiCell's developers.

## Building C++ code
Unlike some other programming languages, for which you simultaneously compile and run your code, in C++ you need to do it separately. PhysiCell offers a quick tutorial on how to set up your computer to compile C++ code. This is further discussed in the [PhysiCell section](physicell-basics/running-code-examples) of the wiki.

The most important component to build the code is the `Makefile`. PhysiCell includes some custom `make` rules that are very useful (for instance, `make data-cleanup` will let you clean your directory by removing all the previous results data). These results are custom, so you can't just use Google to figure out what they do.

You can, however, look into the `Makefile` file, where you will find these rules defined. So, if you are unsure about what rules there are, just look into this file. For instance, the definition for `make data-cleanup` is the following:

```shell
data-cleanup:
	rm -rf ./output
	mkdir ./output
	touch ./output/empty.txt
```

This basically tells us what the `make data-cleanup` command is doing. It deletes the output folder, creates a new one and places a blank txt file inside this folder (`touch` is used to create an empty file). Instead of doing each of these steps manually every single time we want to clean our repository, this rule allows us to do it in a single line of code!

For more information on Makefiles and how to interpret them, you can check [this tutorial](https://makefiletutorial.com).

## Programming language for data analysis
After running the simulations, it will be necessary to process and analyze the results. To do this, currently, the **two best options are Python and MATLAB**, as there are scripts for both these languages that allow you to easily read PhysiCell data.

I personally prefer to use Python and all my code is written in Python, so there are more available resources for this language. However, you can choose between the two. 

In case you have no previous knowledge of either of them, I would strongly recommend learning Python as it is freely available and it is a very powerful tool. My suggestion would be to get familiar with the language and check some of my examples to learn how to apply it to your study.