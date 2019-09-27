---
title: Setup
---

To follow this workshop, you will need three things: MATLAB,
an account on the Supercomputing Wales facility, and an SSH client.

{% comment %} {% endcomment %}

## MATLAB
MATLAB is a popular programming platform for scientific computing.
In this lesson we will be using MATLAB along with its Parallel Computing Toolbox.

### Installation
If you do not already have MATLAB installed on your PC, then you
can install a student version of MATLAB by following the installation
instructions provided at [Install MATLAB](https://myuni.swansea.ac.uk/it-services/software-enquiry/).

If you already have MATLAB installed on your PC, then make sure
that you have the Parallel Computing Toolbox installed. To check
if you have this toolbox installed, type `parpool` at the command
prompt. If you have the Parallel Computing Toolbox installed, then this
command will start a parallel pool. Otherwise, you can install the
toolbox by using the MATLAB's installation executable.

## Supercomputing Wales

In this workshop we will use the Supercomputing Wales facilities to
learn to use High-Performance Computing. For this, you will need an
account on the Supercomputing Wales facilities.

If you already have previously attended the "Introduction to High
Performance Computing" training, and so have already joined the
"scw1389" project, please contact {{site.email}} and we will
reactivate your membership.

If you are new to SA2C training events, create an account through
the following steps:
1. Visit [My Supercomputing Wales](https://scw.bangor.ac.uk/en/accounts/login/?next=/en/)
2. Sign in with your Swansea University email and password.
3. Fill in the form requesting a Supercomputing Wales account.
   Your account request will be processed by an administrator.
4. Once you receive an email indicating that your account has been
   created, revisit [My Supercomputing Wales](https://scw.bangor.ac.uk/en/accounts/login/?next=/en/),
   and log in again if necessary.
5. Click the "Reset SCW Password" button, and enter a password that
   you will use to access the Supercomputing Wales hardware.
   (This does not have to be the same as your Swansea University password.) Click Submit.
6. Under "Join a project", enter "scw1389" as the project
   code for this training session, and click "Join".


{% comment %} End of 'Supercomputing Wales' section. {% endcomment %}
{% comment %} {% endcomment %}

## SSH
SSH is used to connect to the Unix shell on machines across the network.

### Windows
1. If you are using Windows and have previously followed the Unix Shell lesson, then the Git Bash tool installed as part of that lesson will provide you with this.
2. Otherwise, download and install PuTTY.

### MacOS
1. SSH is installed as part of macOS and is available via the Terminal application.

### Linux
1. SSH is installed as part of Linux and is available through a Terminal/Console application.


{% comment %} End of 'SSH' section {% endcomment %}


{% include links.md %}
