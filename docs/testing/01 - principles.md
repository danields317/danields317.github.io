# Principles
Proper testing follows multiple principles and fundamental ideas. These concepts help to think about tests in a practical and realistic way.
## Test Objectives
There are multiple different goals of running tests, some of the most typical are:
- Evaluating that code works as is requested by the requirements
- Triggering failures to test error flows
- Ensuring required test coverage
- Reducing risks
- Verifying legal requirements
- Providing information to stakeholders
- Build confidence for the quality of the code
### Testing and Debugging
Testing and debugging are different activities. Testing is concerned with triggering failures and identifying issues. Debugging is the process of finding out why the software then fails and how it should be resolved.
### Testing and Quality Assurance
Testing is a part of the QA process. Test results can be used during quality control to fix issues.
## Errors, Defects, Failures and Root Causes
- An **error** is a mistakes made during implementation (so human error or AI error)
	- Usually code, but could also be a documentation mistake.
- A **defect** is a problem in the system caused by the error (bugs, faults).
- A **failure** is an event where software does not behave as expected.
	- Usually due to an error/defect, but can also happen without human error (e.g. power outage)
- A Root cause is the fundamental reason that a failure happened.
## Test principles
1. Testing shows the presence, not the absence of defects.
	- Even when adding a million passing tests, it is still possible that there is a defect in an untested case.
2. Exhaustive testing is impossible
	- Except for trivial cases, it is impossible to test every single possible situation.
3. Early testing saves time and money
	- Defects removed early will not cause subsequent defects, which would take more time to solve
4. Defects cluster together
	- There is usually one part in the software that contains the most defects (pareto principle, 80/20 rule).
5. Testing wears out
	- Old tests might still work even when new logic is build on top of the code, but the old test might not be able to catch issues in the newer logic.
6. Testing is context dependent
	- It always depends on the context in which software is build to decide how tests should be done.
7. Absence-of-defects fallacy
	- Even a perfectly bug-free system can be unusable when it does not meet the requirements from the business case. So code testing should not be seen as the silver bullet to solve everything.
## Test activities
While testing is always done differently based on the context, some generic concepts will usually be present:
- Test planning
	- Defining what the goals are when testing and how it should be done.
- Test monitoring and control
	- Checking if actual test activities match the actions defined in the plan (monitoring). Taking the needed actions to meet the goals defined in the plan (control).
- Test analysis
	- Analysis to identify what features should be tested and the expected risk of issues on the feature. It answers: What to test?
- Test design
	- Define how the test should be performed. Which data should be used and what result is then expected. It answers: How to test it?
- Test implementation
	- The creation of the tests. Includes creation the environment, test data etc.
- Test execution
	- Running the tests. How this is done depends on the context and type of tests.
- Test completion
	- After tests are run, useful reports should be stored and any needed cleanup should be done.

How all these concepts are implemented depends on the context and options. E.g: stakeholders might decide what should be tested and how much, the used programming language decides what tools can be used, etc.
### Testware
Testware is the name for the work products created during the testing process. In each phase of testing, different testware can be created. E.g: test plans, schedules and criteria can be made before the tests. Logs, completion reports and stacktraces can be created during and after the tests.

### Traceability
It is important that there is a clear connection between the different activities in test phases. E.g. it needs to be clear which unit test is testing a feature described in the test plan.
Traceability will help to ensure plans are properly executed and when changes are made in the future, related items are easier to retrieve.

### Test roles
There are two main roles in testing:
- Test manager
	- Responsible for managing the overall process.
- Tester
	- Responsible for technical implementation and execution.
### Testing good practices
- A tester should have good technical knowledge and test concept logic
- A tester should have good communication skills to explain issues to developers in an understanding and constructive way.

### Tester independence
A tester can be the developer of the code, a team member, someone in the corporation or someone from outside of the corporation. More independence means less bias in tests, but also less communication and understanding.