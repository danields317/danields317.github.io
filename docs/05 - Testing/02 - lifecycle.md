# Lifecycle
Testing is part of the software development lifecycle. Depending on the chosen Software Development approach (Agile, waterfall, etc.), the test approach is adapted.
But all development lifecycles have certain practices that are good to keep in mind.
## Good practices
- A test activity is made for each development activity.
- Different test levels have specific and different test objectives.
- Test analysis and design begins as soon as possible for the activity to test.
- Testers are involved in reviewing as soon as possible.
## Testing as a development driver
There are approaches to use tests as the steering factor when developing software that could be used.

**Test Driven Development (TDD).**
- Technique in which unit tests are written first and code is written afterwards to make the tests succeed.
**Acceptance Test Driven Development (ATDD)**
- Specific tests are written for the specific acceptance criteria.
- Code is written to satisfy these tests.
**Behavior Driven Development (BDD)**
- Tests are first written down in human language to describe expected behavior.
- Automatic tests are then created for the described test cases.
## DevOps and testing
Development teams these days usually work in a DevOps way. This helps with the execution of tests since they can usually be automated in the CI/CD pipelines. But these tools do need to be maintained and manual testing can be more difficult sometimes.
## Shift-Left approach
The shift-left approach means to test early during development, but not neglecting later testing either. There is no clear-cut way of implementing shift-left. But some good practices are:
- Reviewing software requirements/specifications from a testing perspective. This can help find ambiguities, incompleteness, inconsistencies, etc.
- Writing tests before functionality is written.
- Using CI/CD for executing tests.
- Using static test tools.
- Performing non-functional testing at component test level.
## Retrospectives and improvement
Retrospectives (E.g. Agile Scrum retro) should be used to discuss testing progress and look for improvements.
## Test Levels
Testing can be done on 5 different levels. A level can be described as a group of test activities on the same abstraction level.
- **Component testing (A.K.A. Unit Testing)**: Testing individual software components. E.g. a function.
- **Component Integration Testing**: Testing of the integration between multiple components. E.g. a class creating an instance of another class and calling a function in it.
- **System testing**: Testing of the functionality exposed by the finished system.
- **System Integration Testing**: Testing of the integration of the system with another system.
- **Acceptance Testing**: Validation of the system to test if it fulfils the user's business needs.
## Test Types
There are two main types of tests.
### Functional Testing
Tests if the code does what it is supposed to do. 
### Non-functional Testing
Tests that verify how well the system behaves. ISO/IEC 25010 specifies the following list of non-functional requirements:
- Performance efficiency
- Compatibility
- Usability
- Reliability 
- Security
- Maintainability
- Portability
### Black Box Testing
Testing done by using external resources to figure out what can be tested. Main goal is to test if the code works according to its specifications.
### White Box Testing
Testing done with knowledge of the code. Main goal is to test if the written code is performing as expected.
### Confirmation testing
Technique to test if new code or allegedly fixed bugs are working properly. Confirmation testing can be done in two ways:
- Running existing tests to verify previously failing tests pass.
- Writing new tests to cover the changes needed.
### Regression testing
Technique to test if code that has not been touched still works properly after a change. Done by running other test cases and verifying none of them fail.
### Maintenance testing
Maintenance can be categorized as corrective (fixing issues), adaptive (change in configuration), improvement (upgrading systems). Maintenance testing is the technique to test if a change won't break anything. It depends on the change what activities need to be performed. E.g. when upgrading a stand-alone application less tests have to be done then when a database that is connected with multiple applications gets upgraded.