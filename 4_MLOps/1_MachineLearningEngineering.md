## Machine Learning Engineering

Collection of MLOps best practices, to have a ML app runnable and scalable.

First best practice is using **microservices** opposed to the monolitich approach.
The, **CD** enables the code to always be deployable.

Example pipeline: source code in Github, build in AWS CodeBuild (IAC) and deployment in AWS Beanstalk (serverless). *AWS Elastic Beanstalk* creates an environment that runs a version of your application, managing: capacity provisioning, load balancing...

**AWS App Runner**: add source, configure and build, verify and create url for the final dashboar. From Console, check which apps are running, with links and metrics.
 Source can be a Github repo or a container image, for example stored in **AWS ECR** (Elastic Container Registry). Build can be manual or automatic through a configuration file. App Runner manages load and also monitors health status.
