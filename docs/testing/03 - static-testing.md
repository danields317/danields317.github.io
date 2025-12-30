# Static testing
Static testing is the process of testing code without executing it. The tests are performed by manual evaluating or with the help of tools.

Almost all work products can be reviewed through static testing. As long as the product is humanly readable, static testing is possible. E.g. written code, test plan, user story.

Static analysis can only be performed when a predefined structure it should match is available. E.g. a linter can perform static analysis on code because a certain syntax should be followed. A spellchecker can check grammar mistakes because of linguistic rules.

Static testing is valuable because it helps catch errors very early in development since the only required product is humanly readable text. No working code or environment has to be created to perform some kind of static testing.
Manual static testing can be costly due to the need for human labor, but testing with tools is quick and efficient.
## Static vs Dynamic testing
While both types are meant to reduce errors, there are some differences in usage:
- Some errors can only be found by either static or dynamic testing.
- Static testing finds errors directly while dynamic testing finds them through creating failures.
- Static testing may more easily detect issues in rarely used flows in the software.
- Static testing can be applied to non-executable products.
- Static testing can measure qualities not dependent on running the software (e.g. maintainability)
Main benefits of static testing:
- Find defects in requirements documentation (inconsistency, ambiguity).
- Design issues.
- Syntax errors.
- Deviation from standards (e.g. not following SOLID rules).
- Specific security vulnerabilities.
- Test coverage issues.
## Review process
Reviewing often can help catch issues before they escalate. Involving the stakeholders in this process is valuable to ensure that business requirements are part of the review process.
### Activities
The ISO 20246 describes multiple steps for a proper review process.
- **Planning**: Activity in which the scope of the review gets set. E.g. what product is reviewed? What (non-)functional requirements where expected? etc.
- **Review initiation**: Activity to confirm that everything is properly set up to review. E.g. everyone involved has the correct access, knowledge and understanding of their roles.
- **Individual review**: Each assigned review individually review the product and logs their review.
- **Communication and analysis**: Everything found in the reviews is discussed and action items are created based on the reviews (items can also not be picked up if unnecessary).
- **Fixing and reporting**: The action points are executed and their results is reported on to document the final state of the work product.
### Roles
There are multiple roles in a review. One person can have multiple roles.
- **Manager**: Decides what to review and how it should be done.
- **Author**: Creator of the work product to review.
- **Moderator**: Facilitates the meetings for reviewing and ensures smooth process.
- **Scribe**: Documents discussions input and output.
- **Reviewer**: Someone performing review on work product.
- **Review leader**: Decides who is going to review and organizes the review task.
### Review types
- **Informal review**: No defined process and mostly to detect anomalies.
- **Walkthrough**: Session led by the work product author to share information or ideas.
- **Technical review**: Review done by qualified technical experts. Done to check any type of technical issue.
- **Inspection**: Follows all the steps described above. Done to gain as much information about the work product as possible.

