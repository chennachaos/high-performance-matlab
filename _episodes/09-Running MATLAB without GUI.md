---
title: "Running MATLAB without GUI"
teaching: 30
exercises: 10
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
- "Use 'matlab <mfile.m>')"
---

# Running a MATLAB script from the command line
Many users of MATLAB often use it interactively via a graphical user interface (GUI) to debug and run programs. This is not an effective approach when we use MATLAB on a supercomputer or automate the task of running multiple simulations simultaneously, for example, running the same program with different input files.

MATLAB users are usually accustomed to using MATLAB interactively via its GUI. While MATLAB can be loaded on a supercomputing machine in GUI mode, it is not a recommended practice as its performance is heavily dependent on the internet speed and local X-Windows implemention.

> ## Recommended practice
To prototype and test your code on a personal computer and then port your code to HPC machine.
{: .callout}

Assuming that the MATLAB script file `matlabtest.m` is located in the present working directory, we use the following command to run MATLAB from the commandline.
~~~
matlab -nosplash -nodesktop -nodisplay -r "run(matlabtest.m); quit;" > MatlabRun.out
~~~
{: .language-bash}

> ## Callout Title
> * `matlab` is the MATLAB executable
> * `-nosplash` prevents MATLAB from displaying the splash screen (logo, version, etc..)
> * `-nodesktop` starts MATLAB without the desktop environment
> * `-nodisplay` suppresses the display of figures during MATLAB execution
> * `-r` tells MATLAB to start running the specified command (or the script file with the list of commands)
> * `"run(matlabtest.m); quit;"` MATLAB commands to run. If `quit` is not specified then the MATLAB session will remain open.
> * `>` Output redirection
> * `MatlabRun.out` The file to which the output is redirected to
{: .callout}


{% include links.md %}

