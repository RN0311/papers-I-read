## Data Centric Performance Measurement Techniques for Chapel Programs
###### Introduction
> Chapel is an emerging PGAS(Partitioned Global Address Space) language whose design goal is to make parallel 
programming more productive and generally accessible.This paper exposes data-centric new optimization opportunities 
that are useful in resolving data locality problems.
Since performance is critical in HPC programming, but it is difficult to identify the inefficiencies and 
performance bottlenecks of high-level applications at the source code level.
###### State of the art
> Traditional code-centric view of performance data lacks the capability to find performance problems 
associated with the different variables accessedby specific lines of code.Present, data-centric approaches which 
relate performance to data structures rather than code regions are especially important for HPC/PGAS since memory allocation and data movement are often the key bottlenecks.So, the dire need for a profiling tool which can identify inefficiencies by memory regions. 
###### Overview
> This paper signifies the fact that thee aren't any performance analysis tools which support Chapels' 
unique language features and to be able to associate performance statistics to 
source code variables, not just functions, we need data-centric way to map and present the profiling data.
Further, they introduced the data-centric approach which builds on a performance mapping technique called as 
**"variable blame"**.<br > A variable's blame is a percetage that indicates the share of certain performance metrics, such as time, cache misses and I/O operations due to individual variables.<br >
Blame is an inclusive data-centric method that utilizes the control flow and full data flow information to map
performance data all back to variables in the source code. Also, authors elegantly give detailed discription for calculating blame, which comprises of four steps, combining static(pre-run) information and dynamic(runtime) information of a 
binary to map performance data to variables in the source code.
###### Conclusion
> In nutshell, this paper introduced a state of art profiling tool to analyze performance issues of HPC/PGAS programs.
And highlights that as compared to traditional code-centric profilers a data centric profiler exposes the performance 
bottlenecks from a different view thus giving application programmers more insights to address performance issues.
