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

Bottom-Up Method
The bottom to up testing strategy deals with the process in which lower
level modules are tested with higher level modules until the successful
completion of testing of all the modules. Top level critical modules are
tested at last, so it may cause a defect. Or we can say that we will be
adding the modules from bottom to the top and check the data flow in the
same order

Advantages
o Identification of defect is easy.
o Do not need to wait for the development of all the modules as it saves
time.
Disadvantages
o Critical modules are tested last due to which the defects can occur.
o There is no possibility of an early prototype.

NON- INCREMENTAL INTEGRATION TESTING
We will go for this method, when the data flow is very complex and when it
is difficult to find who is a parent and who is a child. And in such case, we
will create the data in any module bang on all other existing modules and
check if the data is present. Hence, it is also known as the Big bang
method.


Big Bang Method
Big bang integration testing is a testing approach where all components
or modules are integrated and tested as a single unit. This is done after
all modules have been completed and before any system-level testing is
performed


For example, consider a simple system with three modules A, B, and C.
Module A has been tested and found to be working correctly. The same is
true for modules B and C. To test the system as a whole, all three
modules are integrated and tested together.
Since this testing can be done after completion of all modules due to that
testing team has less time for execution of this process so that internally
linked interfaces and high-risk critical modules can be missed easily.


Advantages:
o It is convenient for small size software systems.

Disadvantages:
o Identification of defects is difficult because finding the error where it
came from is a problem, and we don't know the source of the bug.
o Small modules missed easily.
o Time provided for testing is very less.
o We may miss to test some of the interfaces