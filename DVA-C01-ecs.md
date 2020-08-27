# AWS Elastic Container Service

- Needs a task definiton file.

A task placement strategy is an algorithm for selecting instances for task placement or tasks for termination. Task placement strategies can be specified when either running a task or creating a new service.

### ask placement strategies

- `binpack` - Place tasks based on the least available amount of CPU or memory. This minimizes the number of instances in use.
- `random` - Place tasks randomly.
- `spread` - Place tasks evenly based on the specified value. Accepted values are attribute key-value pairs, instanceId, or host. 

## LifeCycle event hooks for an Amazon ECS deployment

AWS Lambda hook is one Lambda function specified with a string on a new line after the name of the lifecycle event.
Each hook is executed once per deployment. Following are descriptions of the lifecycle events where you can run a hook
during an Amazon ECS deployment.

- `BeforeInstall` – run tasks before the replacement task set is created. One target group is associated with the original task set. If an optional test listener is specified, it is associated with the original task set. A rollback is not possible at this point.
- `AfterInstall` – run tasks after the replacement task set is created and one of the target groups is associated with it. If an optional test listener is specified, it is associated with the original task set. The results of a hook function at this lifecycle event can trigger a rollback.
- `AfterAllowTestTraffic` – run tasks after the test listener serves traffic to the replacement task set. The results of a hook function at this point can trigger a rollback.
- `BeforeAllowTraffic` – run tasks after the second target group is associated with the replacement task set, but before traffic is shifted to the replacement task set. The results of a hook function at this lifecycle event can trigger a rollback.
- `AfterAllowTraffic` – run tasks after the second target group serves traffic to the replacement task set. The results of a hook function at this lifecycle event can trigger a rollback.

## Links

- https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-strategies.html
- https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement.html
