---
title: Modules
categories:
 -
layout: docs
---

We maintain a large software stack that is available across all our clusters (licenses permitting).

We use environment modules to let you manage which specific versions of software packages you are using. 

## General use of environment modules

We have a default set of modules that everyone has loaded when they log in: these include the current default compiler and MPI, some utili
ties to make your life easier and some text editors.

### Summary of module commands
```
module avail            # shows available modules
module whatis           # shows available modules with brief explanations
module list             # shows your currently loaded modules

module load <module>    # load this module
module unload <module>  # unload this module
module purge            # unload all modules

module show <module>    # Shows what the module requires and what it sets up
module help <module>    # Shows a longer text description for the software
```

### Find out if a software package is installed and load it

Generically, the way you find out if a piece of software is installed is to run
```
module load beta-modules
module avail packagename
```

By loading `beta-modules` you will also be able to see newer versions of GCC and the software that
has been built using them.

Then `module avail` gives you a list of all the modules we have that match the name you searched 
for. You can then type 
```
module show packagename
```
and it will show you the other software dependencies this module has: these have to be loaded first. It also shows where the software is installed and what environment variables it sets up.

Once you have found the modules you want to load, it is good practice to refer to them using their full name, including the version. If you use the short form (`package` rather than `package/5.1.2/gnu-4.9.2`) then a matching module will be loaded, but if we install a different version, your jobs may begin using the new one and you would not know which version created your results. Different software versions may not be compatible or may have different default settings, so this is undesirable.

You may need to unload current modules in order to load some requirements (eg different compiler, different MPI).

This example switches from Intel compiler and MPI modules to GNU ones.
```
module unload -f compilers mpi
module load compilers/gnu/4.9.2
module load mpi/openmpi/3.1.4/gnu-4.9.2
```
You can use the short name when unloading things because there is usually only one match in your current modules.

The last part of a module name usually tells you what compiler it was built with and which version 
of that compiler. There may be GNU compiler versions and Intel compiler versions of the same 
software available.

Once the module is loaded, you should have all the usual executables in your path, and can use its commands. You load modules in exactly the same way inside a jobscript.