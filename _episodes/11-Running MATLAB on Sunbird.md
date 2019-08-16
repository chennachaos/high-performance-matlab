---
title: "Running MATLAB on Sunbird"
teaching: 30
exercises: 30
questions:
- "Key question (How do I run MATLAB scripts from the commandline)"
objectives:
- "First learning objective. (To run MATLAB scripts from the commandline)"
keypoints:
- "Use `ssh -Y uname@sunbird.swansea.ac.uk` to access Sunbird HPC machine"
- "Use `module load Matlab_Swansea` to load MATLAB software on Sunbird"
---
MATLAB is a multi-paradigm numerical computing platform for scientific computing, and is also a high-level programming language.

MATLAB offers support for linear algebra (Matrices and Vectors), function evaluations, plotting and visualisation, and symbolic computations for mathematical expressions.

Unlike C, C++ and Fortran, MATLAB is an interpreted language similar to Python. This means that programs written in MATLAB can be executed directly without the need for compiling them. Therefore, MATLAB is relatively easy to learn and use compared to compiled languages C, C++ and Fortran. However, the price one has to pay for this functionality is the slowness of computations. MATLAB is atleast an order of magnitude is slower than the programs written in C, C++ and Fortran. Though, MATLAB supports linking of C/C++ and Fortran codes with MATLAB code, if one is interested in replacing computing-intensive routines with C++ or Fortran programs.

## Scope of this lesson

In this workshop we will focuss on the techniques that help run MATLAB programs efficiently and effectively using commandline interface and high-performance computing (HPC) resources. This material is aimed at problems that require 100s or 1000s of simulations with different input parameters to a single programs, and/or problems that are computationally very demanding that each simulation runs for days on personal computers.

We will cover
* The techniques to run multiple simulations with different input parameters to a single MATLAB program, known in the parallel computing community as Single Program Multiple Data (SPMD) technique.
* Improving the performance of MATLAB programs (scripts) using MATLAB's Parallel Computing Toolbox.

## Accessing Sunbird 
The HPC facility that we will be using for today's workshop is **Sunbird**, one of the HPC machines of *Supercomputing Wales* project located in Swansea.

We access Sunbird using the SSH client via commandline. Open a terminal and enter the following command by replacing *uname* with your username.
~~~
ssh -Y uname@sunbird.swansea.ac.uk
~~~
{: .language-bash}
Once you press `Enter` you will probably be asked to type in your password. If you have forgotten your passwork, you can reset it at [My Supercomputing Wales](https://scw.bangor.ac.uk/en/accounts/login/?next=/en/).

Once you successfully log in to Sunbird, you should see some information about Sunbird.

## Using MATLAB on Sunbird

All the libraries and software on HPC machines are available in the form of **modules**. To access a particular software, we have load the corresponding module first.

To use MATLAB, we need to load it first.
~~~
module load Matlab_Swansea
~~~
{: .language-bash}

Executing this command will load the default module for MATLAB. If you want to load a specific version of a software, then you have to specify it to the *module load* command. Refer to [Supercomputing Wales Portal](https://portal.supercomputing.wales/index.php/command-line-environment/) for more details on modules.

We can check the version of MATLAB that is loaded by typing
~~~
module list
~~~
{: .language-bash}

By typing 'which matlab' on the terminal we can check which MATLAB executable is called.
~~~
which matlab
~~~
{: .language-bash}

~~~
/app/languages/MATLAB_Swansea/R2017b/bin/matlab
~~~
{: .output}



{% include links.md %}

