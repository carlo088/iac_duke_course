### Microservices
In general, a DevOps practice. Main advantages: **serverless** (code runs without provisioning servers).
Small, autonomous, specialized, high degree of reliability.
Where can one run a Microservice? In a container or on a cloud service such as AWS Lambda: a serverless compute service that runs your code in response to events

*Flask* Very common, it *maps a python function to a URL*, that's why basic method is @route. 
*API* to define interactions between services.
*JSON* to interchange data.

#### Flask App in Azure
Deploying on Azure: once Flask app is ready, push it to azure with `az webapp up -sku F1 helloflask`.
Now app is on public website and can be accesseed by anyone! From now only, for any local change in source code, just update with `az webapp up`.

#### AWS Serverless Services

##### AWS Lambda
Creat function and specify runtime (like python 3.8). Then add code in *Code* section. Code now lives there and runs when manually executed or when triggered remotely.

**CLI** Lambda function can be triggered from CLI. Just run: `aws lambda invoke --function-name $NAME --payload $FUNCTION_INPUT output.txt`

##### AWS Step Functions
To orchestrate multiple Lambda functions. Also provides *Graph inspector* a graph interface with all the steps.

##### AWS S3 Trigger
Connect S3 to Lambda function, whenever a new file is uploaded inside the bucket, this triggers the function that processes the file.

##### AWS SAM (Serverless Application Model)
Build and app and deploy on AWS Cloud. Tutorial for an Hello World project:
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-getting-started-hello-world.html

Example of Flask Microservice: https://github.com/noahgift/flask-change-microservice

##### AWS CloudWatch - Alert and Monitoring
For Alert and Monitoring. Can be attached for example to a Lambda function to monitor its execution. Or also set a trigger every, say, 1 min.

##### Locust - Load Testing
Test app to evaluate performance and reliance of app. `pip install locust` lets you access a UI at localhost. Here, one can simulate certain number of users using the app simultaneously to verify how infrastructure holds.

#### Promethues - Monitoring




