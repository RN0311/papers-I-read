## Chapel: Cascade High-Productivity Language An Overview of the Chapel Parallel Programming Model∗

### Introduction 
> Chapel, **C**ascade **H**igh-**P**roductivity **L**anguage is a new parallel programming 
language designed with productivty in mind i.e. to advance high-performance computing 
system that is highly productive for its users.This paper gives an overview of the 
Chapel programming model and enumeration of the language's abstractions for data and task-parallelism.
Chapel,abstracts a parallel machine into units of locality called *locales*, and units if execution called 
as threads.
By distinguishing between threads and locales, Chapel is able to support and compose both 
data- and task-parallel programming abstractions.

### Data-Parallel Abstractions
###### Domains
> Chapel distinguishes between the indices over which an array is defined and 
the data within that array by allowing the programmer to abstract them separately. A 
*domain* is an index set with no associated data.
```Chapel
var D : domain(2) = [1..n,1..n],
    IndexD : domain(2) = [2..n-1,2..n-1],
    A,B : [D] float;
```
> Domains support iteration over their index set.
```Chapel
for i,j in IndexD do
  A(i,j) = B(i,j)
```
###### Array Indexing
> Arrays can be indexed by integers where the number of integers is equal to the rank of 
the array.
For example, assignment of the interior elements of B to interior elements of A can bee written as :
```Chapel
for i in IndexD do
  A(i) = B(i)
```
> Chapel also, allows indexing by domains.
```Chapel
A(IndexD) = B(IndexD)
```
### Task-Parallel Abstractions
These concepts enable the user to control which portions of the code are executed 
concurrently and which portions are executed serially.

###### cobegin
> A **cobegin** statement contains a list of statements which are executed concurrently.
```Chapel
cobegin {
  x = analyze();
  y = evolve();
 }
 ```
 > the functions **analyze** and **evolve** are executed concurrently.
###### serial 
> The **serial** statement is used to control whether a parallel statement should be 
executed concurrently or should be serialized.
```Chapel
function sort(A,low,high) { 
  serial (high-low < 100) cobegin {
    sort(A, low, low + (high - low)/2);
    sort(A, low + (high-low)/2 + 1, high);
  }
  merge(A, low, high);
}
```
###### sync 
 > Synchronization variables generalize single assignment variable to permit multiple writes, 
 which is declared using **sync**.
 
 ### Nested Parallelism
 > The data and task parallel abstractions of Chapel can be arbitrarily composed.For example, 
 ```Chapel
 cobegin {
  forall ij in D do
    analyze(A(ij), B(ij));
  forall ij in D do
    C(ij) = evolve(A(ij), B(ij));
 }
 ```
 > there are two conceptual threads spawed to perform two data-parallel computations which may evolve all the locales
 
 ### Conclusion
 > Chapel is  highly general parallel programming language which unifies abstractions for data and task parallelism, 
 allowing abstractions to be arbitrarily composed.
