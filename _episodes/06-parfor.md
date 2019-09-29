---
title: "parfor"
teaching: 20
exercises: 30
questions:
- "How to parallelise for-loops in MATLAB?"
- "What is parfor-loop and how to use it?"
- "What is a parallel pool in MATLAB?"
objectives:
- "To learn to use parfor-loop in MATLAB."
- "To learn to create parallel pools in MATLAB."
keypoints:
- "parfor-loop is the parallel version of the standard
   for-loop in MATLAB."
- "parfor-loop distributes the iterations among the
   workers in the parallel loop."
- "An understanding of array-slicing rules is important
   when working with arrays in parfor-loop."
- "Always parallel the outermost for-loop, unless you have
  a justifiable reason to parallel the inner for-loops"
- "Direct nesting of parfor-loops is not supported in MATLAB"
---
## parfor
**parfor**-loop is the parallel version of the **for**-loop in
MATLAB. In a parfor-loop, the MATLAB parallel server:
* issues the `parfor` command,
* distributes the loop iterations to workers in the parallel pool,
* sends the data to the workers to execute the command,
* collects the data from the workers once the workers successfully finish the computations, and,
* assembles the data received from the workers.

|![](../fig/parfor-workers.png)|
|:--:|
|Image credit: <https://www.slideshare.net/jbhuang/writing-fast-matlab-code>|

To understand `parfor` and assess the performance gains,
we use the example of the eigenvalue problem. We compute the maximum
of the magnitude of eigenvalues of $m$ random matices of size $n\times n$.
The MATLAB code using a standard serial for-loop is shown below:

~~~
clear all;
clc;

m = 50;
n = 500;
a = zeros(m);

tic
for i=1:m
    a(i) = max(abs(eig(rand(n))));
end
toc
~~~
{: .language-matlab}


~~~
Elapsed time is 6.783651 seconds.
~~~
{: .output}

The following MATLAB code extends the previous code to using `parfor`:
~~~
clear all;
clc;

m = 50;
n = 500;
a = zeros(m);

% serial run
%%%%%%%%%%%%

tic
for i=1:m
    a(i) = max(abs(eig(rand(n))));
end
toc

% parallel run
%%%%%%%%%%%%%%

tic
ticBytes(gcp)
parfor i=1:m
    a(i) = max(abs(eig(rand(n))));
end
tocBytes(gcp)
toc
~~~
{: .language-matlab}


~~~
Elapsed time is 6.824506 seconds.
Starting a parallel pool (parpool) using the 'local' profile ...
Connected to the parallel pool (number of workers: 2).
 #    BytesSentToWorkers       BytesReceivedFromWorkers
=======================================================
 1       17928                      12376
 2       17928                      12376
 Total   35856                      24752

Elapsed time is 19.606094 seconds.
~~~
{: .output}

The elapsed time for the parfor-loop is significantly higher than the for-loop.
This is because of an overhead incurred in starting the parallel pool for the first time.
If we run the code for the second time, the elapsed time for the parfor-loop should be lower.

~~~
Elapsed time is 6.792368 seconds.
Starting a parallel pool (parpool) using the 'local' profile ...
Connected to the parallel pool (number of workers: 2).
 #    BytesSentToWorkers       BytesReceivedFromWorkers
=======================================================
 1       20064                      14456
 2       15792                      10296
 Total   35856                      24752

Elapsed time is 3.893476 seconds.
~~~
{: .output}

> ## Data transfer
> Note that the number of bytes sent to and received from workers need not always be equal between the workers.
{: .callout}



> ## Exercise on **parfor**
> The following code populates a 2D array of size `n`$\times$`n`, and
> computes the sum in each row on the fly:
> ~~~
> clc;
> tic
> n = 5;
> A = zeros(n,n);
>
> % serial loop
> for i=1:n
>    for j=1:n
>        A(i,j) = 2*i+3*j;
>    end
>    row_sum = sum(A(i,:));
>    fprintf("%d \t %d \n", i, row_sum)
> end
> toc
> ~~~
> {: .language-matlab}
> We thought of speeding up the calculations by using **parfor**.
> So, we create the following code using **parfor**:
> ~~~
> tic
> A = zeros(n,n);
>
> % parallel loop
> parfor i=1:n
>    for j=1:n
>        A(i,j) = 2*i+3*j;
>    end
>    row_sum = sum(A(i,:));
>    fprintf("%d \t %d \n", i, row_sum)
> end
> toc
> ~~~
> {: .language-matlab}
> When we run the program, we will find out that the
> serial code works but the parallel code does not.
> MATLAB throws an error about `parfor slicing`.
>
>
> Fix the code.
>
> > ## Solution
> > It turns out that we cannot use the array anywhere else in
> > the parfor-loop if we already have used it in a nested for-loop
> > inside the parfor-loop.
> >
> >
> > To fix this, we need to create a temporary 1D array as shown below:
> > ~~~
> > parfor i=1:n
> >    atemp = zeros(1,n);
> >    for j=1:n
> >        atemp(j) = 2*i+3*j;
> >    end
> >    A(i,:) = atemp;
> >    row_sum = sum(A(i,:));
> >    fprintf("%d \t %d \n", i, row_sum)
> > end
> > ~~~
> > {: .language-matlab}
> {: .solution}
{: .challenge}


> ## Array slicing
> Array slicing in MATLAB is nothing but array indexing in MATLAB.
{: .callout}


## When to use parfor
* When the iterations are independent of each other,
  for example, vector and matrix additions.
* When each iteration takes a longer time (this is relative
  and context-dependent) to execute on a single processor.
* In general, loop iterations with computationally intensive
  executions are the candidates for using a parfor-loop, for example,
  the example of computing maximum eigenvalue at the beginning of this episode.


## When not to use parfor
* We might not gain the computational benefits by using parfor-loop if:
    * the loop iterations takes a short time to execute, and,
    * the code has already been vectorised.
* Data dependencies.
  ~~~
  a = 1:100;
  parfor i=2:100
      a(i) = 2.0*a(i-1);
  end
  ~~~
  {: .language-matlab}
  The latest version (2019a) of MATLAB throws an error for this loop, anyway.
* When the number of iterations is lower than the number of workers.
  Otherwise, you do not use all available workers; thus, wasting resources.


> ## parfor-loop index
> parfor-loop indices must be consecutive integers:
> ~~~
> parfor i = 1 : 20        % valid
> parfor i = -10 : 10      % valid
> parfor i = 1 : 3 : 100   % not valid
> ~~~
> {: .language-matlab}
{: .callout}


## Nested parfor-loops
Direct nesting of parfor-loop is not allowed. For example, the
following code is not allowed. Matlab throws an error if you try.

~~~
parfor i = 1:5
    parfor j = 1:100
        ...
    end
end
~~~
{: .language-matlab}

However, a parfor-loop can call a function that contains a 
parfor-loop. But we do not get any additional parallelism 
(computational benefit). To understand that parallelising 
the inner loops adds to the computational overhead, let us
take the following code and measure its performance by 
replacing the for-loops with parfor-loops one at a time.

~~~
n = 100;
A = zeros(n,1);

tic
for i = 1:n  % loop 1
    A(i) = myFunc(i)
end
toc

function val myFunc(i)
    val = 0;
    for j = 1:10  % loop 2
        val = val + 1;
    end
end
~~~
{: .language-matlab}


> ## Exercise on nested par-for loops
> The following Matlab code shows a nested for-loop for computing
> the eigen values.
>
> Measure the performance of the code by appending the code with 
> parfor-loops, first by replacing the outermost loop first and 
> then by replacing the inner loop. Use "ticBytes" and 
> "tocBytes" to also measure the amount of data transfer.
>
> ~~~
> n  = 100;
> ni = 50;
> nj = 50;
> A  = zeros(ni,nj);
>
> tic
> for i = 1:ni
>    for j = 1:nj
>        A(i,j) = max(abs(eig(rand(n))));
>    end
> end
> toc
> ~~~
> {: .language-matlab}
> > ## Solution
> > The timings might vary from one system to the other. But you should
> > observe that parallelsed inner for-loop is expensive when compared
> > to the parallelised outer for-loop.
> > ~~~
> > n  = 100;
> > ni = 50;
> > nj = 50;
> > A  = zeros(ni,nj);
> >
> > tic
> > for i = 1:ni
> >    for j = 1:nj
> >        A(i,j) = max(abs(eig(rand(n))));
> >    end
> > end
> > toc
> >
> > %%%%%%%%%%
> > tic
> > ticBytes(gcp);
> > parfor i = 1:ni
> >    for j = 1:nj
> >        A(i,j) = max(abs(eig(rand(n))));
> >    end
> > end
> > toc
> > tocBytes(gcp);
> >
> > %%%%%%%%%%
> > tic
> > ticBytes(gcp);
> > for i = 1:ni
> >    parfor j = 1:nj
> >        A(i,j) = max(abs(eig(rand(n))));
> >    end
> > end
> > toc
> > tocBytes(gcp);
> > ~~~
> > {: .language-matlab}
> {: .solution}
{: .challenge}


As observed in the examples, parallelising the inner for-loop
does not give any computational benefit. This makes sense
because parallel processing incurs overhead in creating and 
organising the workers in the parallel pool. By parallelising
only the outer loop, such overhead is reduced significantly.

To learn more about parfor-loops, especially their limitations
and fixes for some of the commonly encountered issues, please refer 
to [parfor examples](https://uk.mathworks.com/help/parallel-computing/nested-parfor-loops-and-for-loops.html).

{% include links.md %}
