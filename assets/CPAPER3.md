## OpenML: An R Package to Connect to the Machine Learning Platform OpenML
### Introduction
> OpenML is an online machine learning platform where researchers can easily share data, 
machine learning tasks and experiments as well as organize them online to work and 
collaborate more efficiently.Key elements of OpenML are datasets, tasks, flows and runs: <br >
**Data sets** : OpenML will automatically analyze and annotate the dataets with 
measureable characteristics to support detailed search and further analysis. <br >
**Tasks** : It can be viewd as containers including a dataset and additional information 
defining what is to be learned.They define which input data are given and which 
output data should be obtained.<br >
**Flows** : They are implementations of single machine learning algorithms or whole 
workflows that solve a specific task, eg. a random forest implementation is a flow that 
can be used to solve a classification or regression task.<br >
**Runs**: They are the resullt of executing flows, optionally with preset hyperparameter 
values, on tasks and contain all expected outputs and evaluations of these outputs.(eg. accuracy of predictions)

###### Benefits for society
> OpenML provides a useful learning and working environment for students, scientists and practioners.
Students and scientist can easily explore the state of the art and work together with top minds by 
contributing their own algorithms and experiments.<br >
They can save time, because OpenML assits in many routine and tedious duties: finding datasets, tasks and 
prior results, setting up experiments and organizing all experiments for further analysis.<br >
###### Overview
> OpenML R package is an interface to interact with the OpenML server directly from within R.Users can retireve datasets, tasks, flows and runs from the server from within R.<br >
To interact with the OpenML server, users need to authenticate using an API key, asecret string of characters that uniquely identifies the user.The R package can be easily installed and configured as follows:
```R
install.packages("OpenML")
library("OpenML")
saveOMLConfig(apikey  = "YOUR_API_KEY")
```
> A list of all datasets and tasks that are available on the OpenML server can be obtained using ```listOMLDataSets``` and 
```listOMLTasks``` function respectively.In the example, below a list of all supervised classification tasks based on the data sets having two classes for the target feature, between 500 and 999 instances, at most 100 features and no missing values is shown:
```R
tasks = listOMLTasks(task.type = "Supervised Classification",
number.of.classes = 2,number.of.instances = c(500,999),
number.of.features = c(1,100), number.of.missing.values = 0)
```
```R
tasks[1:2, c("task.id","name","number.of.instances","number.of.features")]
```
> The ```tagOMLObject``` function is able to tag datasets, tasks, flows and runs with a user-defined string, so that 
finding OpenML objects with a specific tag becomes easier.<br >
For example, the task with ID1 can be tagged as follows:
```R 
tagOMLObject(id = 1, object = "task", tags = "test-tagging")
```
> To retrieve a list of objects with a given tag, the tag argument of the listing functions can be used.

###### Conclusion
> OpenML is an online platform for open machine learning that is aimed at connecting 
researchers who deal with any part of the machine learning workflow. The openML platform 
automates the sahring of machine learning tasks and experiments through the tools that scientists 
are already using such as R.

