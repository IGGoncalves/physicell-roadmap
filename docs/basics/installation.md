# Installing PhysiCell

## Setting up a development environemt for Windows users

If you are following PhysiCell's original tutorials from the MathCancer blog, you might have come across the [post](http://www.mathcancer.org/blog/setting-up-a-64-bit-gcc-environment-on-windows/) on how to set up a GCC environment on Windows with MinGW. However, this previous method can lead to some installation issues and it is currently suggested to use MSYS2 instead.

For a video tutorial on installing MSYS2, check out this video from PhysiCell's 2021 Workshop:

[![physicell-lecture](https://img.youtube.com/vi/Jp3ZOMt761M/0.jpg)](https://www.youtube.com/watch?v=Jp3ZOMt761M)

### Video summary + tests

#### Installing MSYS2

Firstly, you should get the installer from the [MSYS2 website](https://www.msys2.org/). Once it has been downloaded, you can **run the installer and just go with the default options** (click on "Next" every time it is aked). At the end of the installation, a command prompt window will pop up. **Copy and paste the following command** into the command prompt:

```bash
pacman -S mingw-w64-x86_64-binutils mingw-w64-x86_64-gcc mingw-w64-x86_64-headers-git mingw-w64-x86_64-gcc-libs mingw-w64-x86_64-libwinpthread-git mingw-w64-x86_64-winpthreads-git mingw-w64-x86_64-lapack mingw-w64-x86_64-openblas mingw-w64-x86_64-libxml2 mingw-w64-x86_64-bzip2 git make
```

You will be asked if you want to install some libraries. You should reply with **"y" or "yes"**. Please, wait for all the libraries to be installed and then you can close the MSYS2 command prompt.

#### Adding directories to PATH

Use the Windows search bar to look for "Environment variables" and select the **"Edit the system environment variables option"**. In the "System variables" winow, select "Path" and then click on "Edit...". Then, press "New" and add the following path:

```
C:\msys64\mingw64\bin
````

Repeat this process to add `C:\msys64\usr\bin` and `.\addons\libRoadrunner\roadrunner\bin` to PATH. Lastly, select these variables and press "Move Up" until they are on the top of the list.

#### Testing out the development environment
In the video, the compiler is tested with PhysiCell straightaway. Yet, we can test it with a simpler script just to be sure that everything is alright, as it was done in the original installation tutorial. Let's try out a simple Hello, World script.

First, creat a new directory and move inside this folder by running these commands in your system's command prompt:

```bash
mkdir hello && cd hello
```

Now, create and save a `hello.cpp` file (you can use any text editor of your choice):

```cpp
#include<iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

as well as a `Makefile`:

```bash
# the compiler: gcc for C program, define as g++ for C++
CC = g++

# compiler flags:
#  -g     - this flag adds debugging information to the executable file
#  -Wall  - this flag is used to turn on most compiler warnings
CFLAGS  = -g -Wall

# The build target 
TARGET = hello

all: $(TARGET)

$(TARGET): $(TARGET).cpp
		    $(CC) $(CFLAGS) -o $(TARGET) $(TARGET).cpp

clean:
			$(RM) $(TARGET)
```

If everything is working correctly, you should be able to run the command `make` in the command prompt and it will print out "Hello, World!".

*Note: if you are not familiar with these commands, you might want to check out the [Programming Review section](../programming-review.md) of this wiki.*

#### Testing PhysiCell examples

You should now be ready to run some of PhysiCell's custom projects. Just move into your PhysiCell directory and run one of the `make [project]` commands, for example `make template`. Then, run `make` and `project.exe`.