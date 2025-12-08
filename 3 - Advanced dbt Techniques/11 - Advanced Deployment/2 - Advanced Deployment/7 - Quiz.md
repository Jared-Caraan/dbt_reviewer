Which of the following best describes the direct promotion (one trunk) strategy in dbt Cloud?

a. Merging feature branches directly into an intermediate QA branch before production.\
b. Merging feature branches directly into the main branch for immediate production deployment.\
c. Merging feature branches into the main branch, followed by additional testing in a QA branch.\
d. Using an external orchestrator to trigger dbt jobs in the cloud.

Answer: b

##
What is the primary risk associated with the direct promotion strategy?

a. The inability to deploy changes automatically.\
b. Automated testing is not available.\
c. There is a risk of deploying untested or faulty code to production.\
d. Jobs cannot be scheduled.

Answer: c

##
In the many trunk (indirect promotion) strategy, what is the purpose of the QA branch?

a. To merge changes directly into production.\
b. To act as a staging area for additional testing before merging into the main branch.\
c. To deploy code directly into production from the QA branch.\
d. To hold unused or archived branches for documentation purposes.

Answer: b

##
Which of the following is a benefit of using the many trunk (indirect promotion) strategy?

a. Changes are deployed immediately after a feature is merged.\
b. Fewer branches are needed, reducing complexity.\
c. Additional testing in the QA environment helps catch potential issues before production.\
d. No need for any scheduled jobs, as changes are deployed automatically

Answer: c
