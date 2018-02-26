### Authoring User-Defined Domain Maps in Chapel∗
###### Introduction
> This paper, unravels one of most promising feature of the Chapel parallel programming language i.e user-defined
domain maps, which give advanced users control over how arrays are implemented and summarized the framework.Since, Chapel's 
main goal is to greatly improve upon the degree of programmability and generality provided by current technologies, while 
supporting performance and portability that is similar or better. <br > <br >
In Chapel, these user-defined array implementations are known as *domain maps* because they map a domain—Chapel’s representation of an 
array’s index set—down to the target machine. Domain maps that target a single shared memory segment are known as *layouts* while those that
target multiple distinct memory segments are referred to as *distributions*.
Lets' consider the following scaled vector addition example:
```Chapel
const D = [1..n];  //the problem statement
var A, B, C: [D] real; //the three vectors
A = B + alpha * C; //the computation
```
> In above, the domain D is declared without any domain map 
specification.So, it is implemented using Chapel's default 
layout.<br >
To target a large-scale distributed-memory system, we can 
simply change the domain's value to include a distribution:
```Chapel

const D = [1..n] dmapped Cyclic(startIdx=1);
var A,B,C: [D] real; //the three vectors
A = B + alpha*C; //the computation
```
> And block distribution will look like as:
```Chapel
const D = [1..n] dmapped Block([1..n]);
var A, B, C: [D] real; //the three vectors
A = B + alpha*C; //the computation
```
###### Overview
> Chapel was designed with a multisolution approach in which 
higher-level features such as parallel arrays and domain maps are 
built in terms of lower-level features that support task parallelism, 
locality, iteration and traditional language concepts.

###### Arrays, Domains and Domain Maps
> **A Chapel array** is a one-to-one mapping from an index set
to a set of variables of arbitrary but homogeneous type.
Chapel arrays are defined using a domain—a first-class
language concept representing an index set.<br >
**Chapel domain maps** specify the implementation of do-
mains and their associated arrays in the Chapel language. If
a domain map targets a single locale’s memory, it is called
a layout. If the domain map targets a number of locales we
refer to it as a distribution.<br >
**Layouts** tend to focus on details like how a domain’s in-
dices or array’s elements are stored in memory; or how a
parallel iteration over the domain or array should be im-
plemented using local processor resources.<br >
Chapel also, supports **subdomain** declarations, which 
support semantic reasoning about index subsets.
Let's understand through an example, cyclic distibution 
followed by a pair of aligned domains D1 and D2 followed 
by a pair of arrays for each domain:
```Chapel
 const M = new dmap(new Cyclic(...));
 const D1 = [0..n+1] dmapped M,
       D2 = [1..n] dmapped M;
       
  var A1,B1: = [D1] int,
      A2,B2: = [D2] real;
 ```
 > Paper, highlights the core part of Domain Map Framework i.e. 
 creating a user-defined domain map in Chapel involves writing a 
 set of three descriptors that collectively implement Chapel's Domain map Standard Interface that are :
 **Domain Map Descriptors**, **Array Descriptors** and **Domain Descriptors**.
 ###### Conclusion
 > In nutshell, this paper describes Chapel's framework for user-defined domain maps to support a 
 flexible means for users to implement their own parallel data structures which support 
 Chapel's global-view operations.




