---
title: "Running MATLAB on Sunbird"
teaching: 20
exercises: 20
questions:
- "How do I run MATLAB scripts from the command line?"
- "How do I run MATLAB from Sunbird?"
objectives:
- "To learn to use HPC resources for MATLAB programs."
- "To run MATLAB scripts from the command line."
keypoints:
- "Use `ssh -Y uname@sunbird.swansea.ac.uk` to access Sunbird HPC machine."
- "Use `module load matlab/2019a` to load MATLAB software on Sunbird."
- "Use `matlab -nosplash -nodesktop -nodisplay -r \"run(matlabtest.m); quit;\"`
  to run matlab script `matlabtest.m` from command line."
---

## Accessing Sunbird
The HPC facility that we will be using for today's workshop is
**Sunbird**, the HPC machine of *Supercomputing Wales* project located
in Swansea.

We access Sunbird using the SSH client via the command line. Open a terminal
and enter the following command by replacing *uname* with your username:
~~~
ssh -Y uname@sunbird.swansea.ac.uk
~~~
{: .language-bash}
Once you press `Enter` you will probably be asked to type in your password.
If you have forgotten your password, you can reset it here:
[My Supercomputing Wales](https://scw.bangor.ac.uk/en/accounts/login/?next=/en/).

Once you successfully log in to Sunbird, you should see some information
about **Sunbird**'s usage, and also notice that the prompt has changed to
`uname@sl1` or `uname@sl2`.

## Using MATLAB on Sunbird

All the libraries and software on HPC machines are available in the
form of **modules**. To access a particular software, we have to load
the corresponding module first.

To use MATLAB, we need to load it first.
~~~
module load matlab/R2019a
~~~
{: .language-bash}

If you want to load a different version, then you have to specify
with the *module load* command. Refer to
[Supercomputing Wales Portal](https://portal.supercomputing.wales/index.php/command-line-environment/)
for more details on modules.

We can check the version of MATLAB that is loaded by typing:
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
/apps/local/languages/matlab/2019a/bin/matlab
~~~
{: .output}


## Running a MATLAB script from the command line
Many users of MATLAB often use it interactively via a Graphical User
Interface (GUI) to debug and run programs. This is not an effective
approach when we use MATLAB on a supercomputer. While it is possible
to open MATLAB on a supercomputing machine in GUI mode, it is not a
recommended practice since its performance is heavily dependent on the
internet speed and local X-Windows implementation.

Create `matlabtest.m` file in the present working directory
 with the Matlab code

~~~
fprintf('The program has started \n\n');

a = 2;
b = 3;
fprintf('Sum of %d and %d = %d \n\n', a, b, (a+b));

fprintf('The program has finished \n');
~~~
{: .language-bash}

We use the following command to run the MATLAB script in
`matlabtest.m` file from the command line.
(*Don't run it yet on Sunbird as executing this
command now will run matlab on the login node which we must avoid.*)
~~~
matlab -nosplash -nodesktop -nodisplay -r "run('matlabtest.m'); quit;"
~~~
{: .language-bash}

> ## MATLAB Command line options
> * `matlab` is the MATLAB executable.
> * `-nosplash` prevents MATLAB from displaying the splash screen (logo, version, etc..).
> * `-nodesktop` starts MATLAB without the desktop environment.
> * `-nodisplay` suppresses the display of figures during MATLAB execution.
> * `-r` tells MATLAB to start running the specified command (or the script file with the list of commands).
> * `"run('matlabtest.m'); quit;"` MATLAB commands to run. If `quit` is not specified then the MATLAB session will remain open.
{: .callout}

You can also use this functionality on your local computers.
On Windows OS use the following command:
~~~
"C:\replace with path to MATLAB installation folder\matlab.exe" -nosplash -nodesktop -nodisplay -r "run('matlabtest.m'); quit;"
~~~
{: .language-bash}


# SLURM
To run a MATLAB program on Sunbird, we first have to prepare a
job script. Using the `nano` editor, we can create a job script file
`matlabjob.sh` using the command:

~~~
nano matlabjob.sh
~~~
{: .language-bash}

and then enter the following text:
~~~
#!/bin/bash --login
###

# job name
#SBATCH --job-name=hostname

# job stdout file
#SBATCH --output=hostname.out.%J

# job stderr file
#SBATCH --error=hostname.err.%J

# maximum job time in D-HH:MM
#SBATCH --time=0-00:10:00

# maximum memory of 10 megabytes
#SBATCH --mem-per-cpu=10

# run a single task, using a single CPU core
#SBATCH --ntasks=1

# specify the current project
# change this for your own work
#SBATCH --account=scw1389

# specify the reservation we have for the training workshop
# replace XX with the code provided by your instructor
# remove this for your own work
#SBATCH --reservation=scw1389_XX
###

# load modules
module load matlab/R2019a

echo "Starting the MATLAB program"

matlab -nosplash -nodesktop -nodisplay -r "run('matlabtest.m'); quit;"

echo "MATLAB program has finished"
~~~
{: .language-bash}


In this way, we need to create the job scripts for the MATLAB programs
that we want to run on HPC machines. There is also an interactive way of
accomplishing this task. You can learn more about this interactive approach
[here](https://edbennett.github.io/SCW-tutorial/04-running-jobs/).
For this course, we will stick to the approach of using job scripts.


{% include links.md %}
