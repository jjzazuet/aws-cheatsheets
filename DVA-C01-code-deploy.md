# AWS Code Deploy

- CodeDeploy Agent.
  - Required only for on-premises or EC2 infrastructure.
  - Not required for Lambda or ECS.
  - Uses outbound HTTPS 443.

https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html#welcome-deployment-overview-blue-green

## Notice
HTTPS 443 only
on-premise - in place only
lambda - blue/green only
ECS - blue/green only
EC2 - both
