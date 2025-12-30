# Dynamic testing
Dynamic testing is the process of running code in one or more test scenario's.
There are multiple techniques and strategies to develop tests. Some of the more common ones are discussed here.
## Black box testing
Black box testing is a technique in which no knowledge of internal working of the system is needed. It only checks the input and output of the system.
### Equivalence partitioning
Equivalence partitioning works with the concept that multiple different values that are expected to behave the same, are in the same partition. 
Testing one of the values in a partition, counts as testing them all.
This is performed by identifying all partitions with the corresponding values and creating a test for each partition.
The values in a partition don't have to be sequential.
### Boundary value analysis
Boundary value analysis tests values on the boundary between partitions (only works in functionality with sequential partitions). 
There are 2 versions of BVA.
2-BVA: Takes the value on the boundary between partitions and the first value in the next partition.
3-BVA: Takes the value on the boundary between partitions, the first value in the next partition and one value underneath the boundary value.

3-BVA is able to catch slightly more issues than 2-BVA.
### Decision table testing
Decision table testing is used when there are multiple input arguments and their combinations should be tested. A table is made which shows the values of each argument and the expected outcome. For each entry, a test case is made.
### State transition testing
State transition testing tests if the software properly changes states when certain events occur. This is done by documenting all states in the software and which events trigger a state change. Different tests can be performed on state transitioning. For example, testing if an event transitions properly, testing if there are no unexpected state changes, etc.
## White box testing
White box testing is a process where the internals of a system are known and more specific tests on the written code are performed.
### Statement testing
A piece of software consists of multiple statements being executed. For example, a function consists of multiple actions, each action is one statement. In statement testing, the proper execution of each different statement is verified.
```
fun doIf(input: num) {
val num = input; // statement 1
if (num > 8) { // statement 2
	println("is larger") // statement 3
}
println("End") // statement 4
}
```
When running a test with input values lower than 8 the statement in the if won't be executed. Reducing the statement coverage. The more coverage the better.
### Branch testing
Branch testing tests if different branches in the code (additional function calls, if blocks) work properly. 
## Experience based testing
Experience based testing is a technique where a tester uses their own intuition to try specific test cases.
### Error guessing
The tester tries specific values or flows of events that they already know might cause issues.
### Exploratory testing
The tester makes up test scenarios and tests them immediately. This is a kind of interactive testing where the tester simply tries out the application and attempts to find out issues on the fly by messing around.
### Checklist based testing
The tester writes down a list of what they want to test and goes past it.
## Collaboration based testing
Techniques to usually prevent issues by working on topics together. This might catch bugs before an official testing task is started.
### Collaborative user story writing
Writing user stories with multiple people can create discussion while creating it. This way, any inconsistencies and issues might be caught during creation.
### Acceptance criteria
Setting up acceptance criteria helps the team understand how a certain task needs to be implemented.
### ATDD
Acceptance test driven development is a process where functionality is made by implementing according to the already prepared acceptance criteria. This way multiple people are involved from the start and discussions can already be started during development instead of only in review afterwards.