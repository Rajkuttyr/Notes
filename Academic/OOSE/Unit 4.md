# INTEGRATION TESTING

1.  Integration testing is the process of testing the interface between two
software units or modules.
2.  The purpose of integration testing is to expose faults in the
interaction between integrated units
3. Once all the modules have been
unit-tested, integration testing is performed.

4. t helps to identify and resolve integration issues early in
the development cycle, reducing the risk of more severe and costly
problems later on

5. Types of Integration Testing
Integration testing can be classified into two parts
o Incremental integration testing
o Non-incremental integration testin


![[Pasted image 20260528145929.png]]

Incremental Approach
In the Incremental Approach, modules are added in ascending order one
by one or according to need. The selected modules must be logically
related. Generally, two or more than two modules are added and tested to
determine the correctness of functions. The process continues until the
successful testing of all the modules.

For example: Suppose we have a Flipk art application, we will perform
incremental integration testing, and the flow of the application would like
this:
Flipkart→ Login→ Home → Search→ Add cart→Payment → Logout

Incremental integration testing is carried out by further methods:
o Top-Down approach
o Bottom-Up approach

Top-Down Approach
The top-down testing strategy deals with the process in which higher level
modules are tested with lower level modules until the successful
completion of testing of all the modules. Major design flaws can be
detected and fixed early because critical modules tested first. In this type of
method, we will add the modules incrementally or one by one and check
the data flow in the same order

Advantages:
o Identification of defect is difficult.
o An early prototype is possible.
Disadvantages:
o Due to the high number of stubs, it gets quite complicated.
o Lower level modules are tested inadequately.
o Critical Modules are tested first so that fewer chances of defects.