You now have all the required knowledge to create your own model. However, to simplify the process, I recommend following this workflow.

## Starting with a template
**PhysiCell provides you with many project templates, and it is totally OK to use them as a starting point.** That is why they are there! So, go ahead and think about which one you would like to work it. Personally, I like starting from a blank canvas and use the `template` project, but you can start where you want.

Just go ahead and populate your project with the necessary files by calling `make template`.

## Modifying your code and compiling it
**Do all the necessary changes to your code and compile the project by calling `make`**. Do not be afraid of using the User Guide and other examples to build your custom functions.

In case you make further changes to the code, you will need to recompile it. You do not usually need to recompile all of the files, so you just have to call `make`. However, if some strange error occurs, you can try cleaning the compiled files and start from scratch. You can use `make clean` for this.

**Do not confuse `make clean` with the `make reset` one!** You have to be quite careful with your code when using **make reset**. This will delete all of the code in your main directory. To be safe, **I recommend always having a backup of your code or, even better, using Git.**