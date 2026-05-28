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

REGRESSION TESTING
Regression testing is a black box testing techniques. It is used to
authenticate a code change in the software does not impact the existing
functionality of the product. Regression testing is making sure that the
product works fine with new functionality, bug fixes, or any change in the
existing feature.

Test cases are re-executed
to check the previous functionality of the application is working fine, and the
new changes have not produced any bugs. 

This method is used to test the product for modifications or any updates
done

Verify that the bugs fixed and the newly added
features not created any problem in the previous working version of the
Software.

# SYSTEM TESTING

System testing is a type of software testing that evaluates the
overall functionality and performance of a complete and fully integrated
software solution

 It tests if the system meets the specified requirements
and if it is suitable for delivery to the end-users

This type of testing is
performed after the integration testing and before the acceptance testing.

he goal of integration
testing is to detect any irregularity between the units that are integrated
together

System testing detects defects within both the integrated units
and the whole system

System testing tests the design and behavior of the
system and also the expectations of the customer. 

System Testing is basically performed by a testing
team that is independent of the development team that helps to test the
quality of the system 
It has both functional and non-functional
testing. System Testing is a black-box testing.

ystem Testing Process: System Testing is performed in the following
steps:
 Test Environment Setup: Create testing environment for the better
quality testing.
 Create Test Case: Generate test case for the testing process.
 Create Test Data: Generate the data that is to be tested.
 Execute Test Case: After the generation of the test case and the test
data, test cases are executed.
 Defect Reporting: Defects in the system are detected.
 Regression Testing: It is carried out to test the side effects of the
testing process.
 Log Defects: Defects are fixed in this step.
 Retest: If the test is not successful then again test is performed.

Types of System Testing
 Performance Testing: Performance Testing is a type of software
testing that is carried out to test the speed, scalability, stability and
reliability of the software product or application.
 Load Testing: Load Testing is a type of software Testing which is
carried out to determine the behavior of a system or software product
under extreme load.
 Stress Testing: Stress Testing is a type of software testing performed
to check the robustness of the system under the varying loads.
 Scalability Testing: Scalability Testing is a type of software testing
which is carried out to check the performance of a software application
or system in terms of its capability to scale up or scale down the
number of user request load

Advantages of System Testing
 The testers do not require more knowledge of programming to carry
out this testing.
 It will test the entire product or software so that we will easily detect
the errors or defects which cannot be identified during the unit testing
and integration testing.
 The testing environment is similar to that of the real time production or
business environment.
 It checks the entire functionality of the system with different test
scripts and also it covers the technical and business requirements of
clients.
 After this testing, the product will almost cover all the possible bugs or
errors and hence the development team will confidently go ahead with
acceptance testing

# WHITEBOX TESTING
It tests internal coding
and infrastructure of a software focus on checking of predefined inputs
against expected and desired outputs

In this type of
testing programming skills are required to design test cases

The primary
goal of white box testing is to focus on the flow of inputs and outputs
through the software and strengthening the security of the software

The term 'white box' is used because of the internal perspective of the
system. The clear box or white box or transparent box name denote the
ability to see through the software's outer shell into its inner workings.

Developers do white box testing. In this, the developer will test every line of
the code of the program.

The developers perform the White-box testing and
then send the application or the software to the testing team, where they
will perform the black box testing and verify the application along with the
requirements and identify the bugs and sends it to the developer.
The developer fixes the bugs and does one round of white box testing and
sends it to the testing team. Here, fixing the bugs implies that the bug is
deleted, and the particular feature is working fine on the application.

The white box testing contains various tests, which are as follows:
o Path testing
o Loop testing
o Condition testing
o Testing based on the memory perspective
o Test performance of the program

Path testing
In the path testing, we will write the flow graphs and test all independent
paths. Here writing the flow graph implies that flow graphs are representing
the flow of the program and also show how every program is added with
one another as we can see in the below image:
And test all the independent paths implies that suppose a path from main()
to function G, first set the parameters and test if the program is correct in
that particular path, and in the same way test all other paths and fix the
bugs.

Loop testing
In the loop testing, we will test the loops such as while, for, and do-while,
etc. and also check for ending condition if working correctly and if the size
of the conditions is enough.
For example: we have one program where the developers have given
about 50,000 loops.
1. {
2. while(50,000)
3. ……
4. ……
5. }
We cannot test this program manually for all the 50,000 loops cycle. So we
write a small program that helps for all 50,000 cycles, as we can see in the
below program, that test P is written in the similar language as the source
code program, and this is known as a Unit test. And it is written by the
developers only.

BlackBox TEsting

Black-box testing is a type of software testing in which the tester is not
concerned with the internal knowledge or implementation details of the
software but rather focuses on validating the functionality based on the
provided specifications or requirements.

The technique involves two steps:
1. Identification of equivalence class – Partition any input domain into
a minimum of two sets: valid values and invalid values. For
example, if the valid range is 0 to 100 then select one valid input like
49 and one invalid like 104.
2. Generating test cases – (i) To each valid and invalid class of input
assign a unique identification number. (ii) Write a test case covering
all valid and invalid test cases considering that no two invalid inputs
mask each other. To calculate the square root of a number, the
equivalence classes will be (a) Valid inputs:
 The whole number which is a perfect square-output will be an
integer.
 The entire number which is not a perfect square-output will be a
decimal number.
 Positive decimals
 Negative numbers(integer or decimal).
 Characters other than numbers like “a”,”!”,”;”, etc.
3. Boundary value analysis – Boundaries are very good places for
errors to occur. Hence, if test cases are designed for boundary values of
the input domain then the efficiency of testing improves and the
probability of finding errors also increases. For example – If the valid
range is 10 to 100 then test for 10,100 also apart from valid and invalid
inputs.

. Discovers missing functions, incorrect function & interface errors
2. Discover the errors faced in accessing the database
3. Discovers the errors that occur while initiating & terminating any
functions.
4. Discovers the errors in performance or behaviour of software.
Features of black box testing:
5. Independent testing: Black box testing is performed by testers who
are not involved in the development of the application, which helps to
ensure that testing is unbiased and impartial.
6. Testing from a user’s perspective: Black box testing is conducted
from the perspective of an end user, which helps to ensure that the
application meets user requirements and is easy to use.
7. No knowledge of internal code: Testers performing black box testing
do not have access to the application’s internal code, which allows
them to focus on testing the application’s external behaviour and
functionality.
8. Requirements-based testing: Black box testing is typically based on
the application’s requirements, which helps to ensure that the
application meets the required specifications.
9. Different testing techniques: Black box testing can be performed
using various testing techniques, such as functional testing, usability
testing, acceptance testing, and regression testing.
10. Easy to automate: Black box testing is easy to automate using
various automation tools, which helps to reduce the overall testing
time and effort.
11. Scalability: Black box testing can be scaled up or down depending on
the size and complexity of the application being tested.
12. Limited knowledge of application: Testers performing black box
testing have limited knowledge of the application being tested, which helps to ensure that testing is more representative of how the end
users will interact with the application.

Advantages of Black Box Testing:
 The tester does not need to have more functional knowledge or
programming skills to implement the Black Box Testing.
 It is efficient for implementing the tests in the larger system.
 Tests are executed from the user’s or client’s point of view.
 Test cases are easily reproducible.
 It is used in finding the ambiguity and contradictions in the functional
specifications.
Disadvantages of Black Box Testing:
 There is a possibility of repeating the same tests while implementing
the testing process.
 Without clear functional specifications, test cases are difficult to
implement.
 It is difficult to execute the test cases because of complex inputs at
different stages of testing.
 Sometimes, the reason for the test failure cannot be detected.
 Some programs in the application are not tested.
 It does not reveal the errors in the control structure.
 Working with a large sample space of inputs can be exhaustive and
consumes a lot of time.