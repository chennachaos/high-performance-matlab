---
title: "Vectorization"
teaching: 15
exercises: 15
questions:
- "What is vectorization in MATLAB?"
- "What are the advantages and disadvantages of vectorization?"
objectives:
- "To learn to vectorize your code in MATLAB."
keypoints:
- "Vectorization in MATLAB is about replacing
   loops with appropriate array operations."
- "Vectorized code runs much faster than the code with loops."
- "Vectorization is concise and makes the code
   easier to understand and debug."
---
## Vectorization
*Vectorization* in computer programming is the act of
transforming loop-based scalar operations into operations
over vectors (or arrays). This should not be confused
with [automatic vectorization](https://en.wikipedia.org/wiki/Automatic_vectorization).

It is debatable whether *vectorization* should be part of a course on
High-Performance Computing in MATLAB. However, if your objective is
to improve the performance of your MATLAB code, *vectorization*
is the place to start.

## What is Vectorization in MATLAB?
To understand the concept of vectorization in MATLAB, let us take
the example of adding two square matrices of rank *n*. In scalar languages
such as C, this can be done using a for-loop:
~~~
// scalar operators of array variables using for-loop
//
for(i=0; i<n; i++)
{
  for(j=0; j<n; j++)
    C[i][j] = A[i][j] + B[i][j];
}
~~~
{: .source .language-c}

The syntax for the same operation in MATLAB is:
~~~
% scalar operators of array variables using for-loop

for i:n
    for j:n
        C(i,j) = A(i,j) + B(i,j);
    end
end
~~~
{: .language-matlab}

Unlike C, MATLAB and Fortran are array languages; they support some
basic operations such as addition, subtraction, multiplication and
division by a scalar to variables of type scalars and arrays.
In short, `vectorization generalises some operations to scalars and arrays`.

The vectorized code for the addition of two variables in MATLAB is:
~~~
C = A + B;
~~~
{: .language-matlab}

The above code is valid irrespective of whether the variables `A`, `B`
and `C` are scalars or arrays. The only requirement for array type
variables is that all the arrays are of the same size and shape,
and contain compatible data types.

## Reasons for using Vectorization
* Vectorized code is often faster than the code with loops.
  MATLAB optimises the vectorized code using optimised libraries
  and multi-threading.
* Vectorized code is concise. Therefore, it is easier to understand and debug.

> ## An exercise on vectorization
> The following MATLAB code adds two square matrices of size n:
> ~~~
> n = 100;
> A = rand(n,n);
> B = rand(n,n);
> tic
> for i=1:n
>     for j=1:n
>         C(i,j) = A(i,j) + B(i,j);
>     end
> end
> toc
> ~~~
> {: .language-matlab}
> Append the code with a vectorized version of the for-loop.
Measure the time to check if you gain any computational benefits.
Repeat this by increasing the value of `n` to 1000 and 10000.
> > ## Solution
> > ~~~
> > % vectorized version
> > tic
> > C = A + B;
> > toc
> > ~~~
> > {: .language-matlab}
> Elapsed times vary from computer to computer. However,
you should see significant improvements between the
for-loop code and vectorized code.
> {: .solution}
{: .challenge}

## Period operator
The period operator (`.`) transforms the scalar operators multiplication
(`*`), division (`/`) and power (`^`) into array operators.

Suppose, we want to calcualte the square of each element in an array.
Using the scalar operations and for-loop, we write:
~~~
n = 100;
x = 1:n;
y = x;
for i=1:n
    y(i) = x(i)*x(i)
end
~~~
{: .language-matlab}

The above code can be vectorized as:
~~~
n = 100;
x = 1:n;
y = x.*x;
~~~
{: .language-matlab}


> ## An exercise on array operators
> The following code computes the radius for a set of points
whose X and Y coordinates are given as arrays:
> ~~~
> n = 100;
> x = rand(n,1);
> y = rand(n,1);
> rad = x;
> for i=1:n
>     rad(i) = sqrt(x(i)*x(i) + y(i)*y(i))
> end
> ~~~
> {: .language-matlab}
> Convert it into a vectorized code.
> > ## Solution
> > ~~~
> > n = 100;
> > x = rand(n,1);
> > y = rand(n,1);
> > rad = sqrt(x.*x + y.*y);
> > ~~~
> > {: .language-matlab}
> > Note that the `sqrt` function here is a vectorized function.
Its syntax is the same whether the argument is a scalar or a vector.
> {: .solution}
{: .challenge}

## Logical array operators
If we want to perform logical operations over the elements of a
vector (or matrix), then we can use MATLAB's comparison operators
which accept vectors as input arguments.

To find which elements of an array are positive, we can write:
~~~
A = [0.2 -2.0 1.0 9.0 -11.0 -98.1 -0.1 2.1 7.7];
A > 0
~~~
{: .language-matlab}

~~~
ans =
1x9 logical array
  1  0  1  1  0  0  0  1  1
~~~
{: .output}

Similarly, we can perform element-wise logical operations by using vectorization in MATLAB.

For additional details on vectorization in MATLAB, we suggest the following material:
* <https://uk.mathworks.com/help/matlab/matlab_prog/vectorization.html>
* <http://www-h.eng.cam.ac.uk/help/tpl/programs/Matlab/tricks.html>

## Limitations and disadvantage of vectorization
* Vectorized code poses issues in parallelising the code for distributed computing.
* Sometimes it is difficult to spot bugs when you miss the period operator (`.`),
  especially if you don't know when and where to use the period operator.

{% include links.md %}
