# Activity Management

When applying testing techniques in large software projects, these test activities need to be properly managed. This can be done through multiple activities, documents, meetings, etc.

## Test planning

Test planning is done through a test plan. There are no strict rules what a test plan should contain, but there are some guidelines.
A test plan should contain all the information needed to perform tests. It documents what is going to be tested, how it should be tested and what the passing criteria are. Any other relevant information should also be documented in the test plan (e.g. timeframes, risks, warnings).

## Entry and Exit criteria

Certain activities can only be started when certain Entry Criteria are met. E.g. resources should be available, licenses acquired, code finished.
Exit criteria tell when a task can be marked as done (A.K.A. Definition of Done). E.g. all tests succeed, system has 95% average availability, but also being out of time or budget can be an exit criteria.

## Estimation Techniques

It is handy to estimate how long a task is going to take. Four estimation techniques are described here.

| Technique       | Description                                                                                                                                                                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ratios          | Based on historic data for similar projects, time estimations for different tasks can be made relatively. E.g. if a previous project had 60% development work and 40% test work (or as a 3:2 ratio), it can be expected a new project to be the same.    |
| Extrapolation   | Basing needed work of of previous work. E.g. using the average testing time from the last few sprints for the expected time this sprint.                                                                                                                 |
| Wideband Delphi | Needed time is based on experience from experts which they decide individually. When there are differences in opinion they are discussed in the group and new individual votes are done until consensus is reached. Planning poker is a variant of this. |
| Three-point     | A mathematic technique where an average of the most optimal, most likely and worst case estimations are combined to get a result.                                                                                                                        |

## Prioritization

Executing tests takes time and effort and all tests offer different benefits. Deciding which tests to run first helps executing the process most optimally. Underneath two visualizations that help with prioritization.

### Test pyramid

Different tests cover a different amount of the codebase. Tests high up in the pyramid cover a large amount of the codebase, but not in detail. Tests lower in the pyramid cover smaller but more specific topics.
![Test pyramid](/img/testing/test-pyramid.png)

### Testing quadrant

Tests either focus on business logic or on technical implementation. At the same time, tests can either check if the code runs as expected or if the product works as expected. The four quadrants fill in the types of tests to perform either.
![Test quadrant](/img/testing/test-quadrant.png)

## Risks

Risk is a potential event, hazard, threat, or situation whose occurrence causes an adverse effect. A risk can be characterized by two factors: 
• Risk likelihood – the probability of the risk occurrence (greater than zero and less than one)
• Risk impact (harm) – the consequences of this occurrence

During a project, risks are usually categorized in one of two types: 

| Risk         | Description                                                                                                              |
| ------------ | ------------------------------------------------------------------------------------------------------------------------ |
| Project risk | A risk related to the management and control of the project. E.g. organizational issues, cost issues.                    |
| Product risk | A risk related to the product developed in the project. E.g. missing features, high maintenance costs, illegal features. |
### Risk Analysis
Risk analysis consists of two activities.

| Activity       | Description                          |
| -------------- | ------------------------------------ |
| Identification | Identify the possible risks          |
| Assessment     | Estimate the importance of each risk |
Ideas to measure risk importance are equating: `likelihood * impact` or using a Risk Matrix.
### Risk control
Risks are controlled by **mitigation** through implementing anything that reduces the likelihood and/or impact of the risk. Risk monitoring is the process of verifying that the mitigation activities are effective.
## Defect management
When a test does not succeed, it usually means a defect in the code is found. When these defects are not solved immediately, they should be documented. The following information is recommended: 
- Unique identifier.
- Name and summary.
- Way to reproduce (steps and/or link to the ran test).
- Context of the defect.