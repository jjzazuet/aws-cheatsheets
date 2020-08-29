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

![VPC](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-05-28_11-31-43-d1e6e5be5012c77c39ec15676d410483.png)

To enable console access, add the AWSXrayReadOnlyAccess managed policy to your IAM user.

For local development and testing, create an IAM user with read and write permissions. Generate access keys for the user and store them in the standard AWS SDK location. You can use these credentials with the X-Ray daemon, the AWS CLI, and the AWS SDK.

To deploy your instrumented app to AWS, create an IAM role with write permissions and assign it to the resources running your application. AWSXRayDaemonWriteAccess includes permission to upload traces, and some read permissions as well to support the use of sampling rules.

The read and write policies do not include permission to configure encryption key settings and sampling rules. Use AWSXrayFullAccess to access these settings, or add configuration APIs in a custom policy. For encryption and decryption with a customer managed key that you create, you also need permission to use the key.

On supported platforms, you can use a configuration option to run the X-Ray daemon on the instances in your environment. You can enable the daemon in the Elastic Beanstalk console or by using a configuration file. To upload data to X-Ray, the X-Ray daemon requires IAM permissions in the AWSXrayWriteOnlyAccess managed policy. These permissions are included in the Elastic Beanstalk instance profile.
