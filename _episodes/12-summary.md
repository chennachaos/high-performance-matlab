---
title: "Summary"
teaching: 10
exercises: 0
questions:
- "Which techniques should I use for which types of problem?"
- "What should I do next?"
---

## Summary
We have leant that:
* MATLAB PCT provides a platform for utilising the power of supercomputers.
* **parfor** is a parallelised version of a for-loop.
* **spmd** offers a very flexible environment to develop
  parallel codes in MATLAB.
* We can use `profile` and `mpiprofile` commands to obtain the performance
  statistics of our code.

We also have learnt how to run MATLAB without the GUI and how to access MATLAB
from HPC clusters.


## What next?
We have covered a lot of topics in this course. However, this course is by
no means exhaustive.
This course covers only the basics of some essential features of MATLAB PCT
that will help in improving the performance of your code by exploiting the
parallel computers. It must be super-exciting to try all these techniques
and tools to improve the performance of your MATLAB codes.

There are many features that we have not covered. We can also explore the
use of GPUs in accelerating the performance. The topic of GPU computing
in MATLAB is big enough to be a one-day workshop. See
* <https://blogs.mathworks.com/loren/2012/02/06/using-gpus-in-matlab/>
* <https://uk.mathworks.com/help/parallel-computing/gpu-computing-in-matlab.html>
for details.

## Some tips
For helping you in improving the performance of your code, we have the following
tips:
* Avoid premature optimisations.
* Profile the code before jumping on parallelising. It is important to know
  what to parallelise.
* Follow incremental approach to parallelisation - parallelise your code step
  by step, starting with the most critical function or block of code.
* To track the changes to your code and revert to the working version,
  in case the modifications are not satisfactory, or if you make a mistake,
  use a version control system. We recommend Git. If you are not familiar
  with version control and Git, then we suggest this [Software Carpentry
  course](http://swcarpentry.github.io/git-novice/).
* Prepare tests that will be useful to test your code once you make some
  major changes, so that modifications do not affect the code developed thus
  far; to make sure that the code still works the way it should. These tests can be
  unit tests or integration tests and some program that can verify the output
  of your code.
* You don't have to run the entire simulation. Always use a small data set
  when testing and optimising your code.


## Additional resources
For additional information, we suggest the following resources:

### On MATLAB Parallel Computing Toolbox
* <https://uk.mathworks.com/help/parallel-computing/getting-started-with-parallel-computing-toolbox.html>
* <http://cacs.usc.edu/education/cs596/ParallelComputingWithMATLAB.pdf>
* <https://www.glue.umd.edu/hpcc/help/software/matlab.html>

### On some (best) practices for improving the performance of your code
* <http://www-h.eng.cam.ac.uk/help/tpl/programs/Matlab/tricks.html>
* <https://undocumentedmatlab.com/books/matlab-performance>
* <https://uk.mathworks.com/help/matlab/matlab_prog/techniques-for-improving-performance.html>
* <https://www.slideshare.net/jbhuang/writing-fast-matlab-code>
* <https://uk.mathworks.com/company/newsletters/articles/tips-for-accelerating-matlab-performance.html>
* <http://www.mit.edu/~pwb/cssm/GMPP.pdf>
* <https://vp.research.msu.edu/sites/default/files/2018-08/Speeding_up_MATLAB_Applications.pdf>
* <http://www.csc.kth.se/utbildning/kth/kurser/DN2255/ndiff13/matopt.pdf>
* <http://www.walkingrandomly.com/?cat=53>
