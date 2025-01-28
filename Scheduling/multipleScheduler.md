## Multiple Scheduler

- Scheduler use algo to evenly divide on nodes

- kubernetes is highly extensible we could write our own kubernetes scheduler program. So, our kubernetes cluster can have multiple scheduler at a same time.

- So while creating pod, deploy, we could instruct kubernetes to have pod scheduled by a specific scheduler

- When multiple Scheduler, they must have different name.

