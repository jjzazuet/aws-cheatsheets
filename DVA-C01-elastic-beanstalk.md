# AWS Elastic Beanstalk

- Uses the `eb` cli.
- Uses `.elasticbenastalk/config.yaml` for configuration to specify deployment artifacts.
- Uses files placed in an `.ebextensios` folder.
  - Uses an `xray-daemon.config`.
  - Uses an `env.yaml` file.
  - `Dockerrun.aws.json` - Used for multicontainer Docker environments hosted in EB.
  - `cron.yaml` - used to execute periodic tasks.

Deployment policy – Choose from the following deployment options:

- All at once – Deploy the new version to all instances simultaneously. All instances in your environment are out of service for a short time while the deployment occurs.
- Rolling – Deploy the new version in batches. Each batch is taken out of service during the deployment phase, reducing your environment's capacity by the number of instances in a batch.
- Rolling with additional batch – Deploy the new version in batches, but first launch a new batch of instances to ensure full capacity during the deployment process.
- Immutable – Deploy the new version to a fresh group of instances by performing an immutable update.
- Blue/Green or Traffic splitting – Deploy the new version to a fresh group of instances and temporarily split incoming client traffic between the existing application version and the new one.
