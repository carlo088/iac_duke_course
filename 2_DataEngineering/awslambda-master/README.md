## AWS Lambda
Check available space in Cloud9 environment and eventually run `./resize.sh` to fetch more data.

**Hello World** Build and Deploy
*sam* is a AWS CLI tool.
1.  `sam init` and set specifications
2.  `sam build` from directory builds the docker container
3.  `sam deploy --guided` this deploys i.e. pushes the container that has been built to AWS

### Deploy and Testing (Key Concepts)

Test two ways:

`sam local invoke` pulls the container and tests the function
`sam local start-api` this is to test the API Gateway. Runs at localhost and one can check with `curl http://127.0.0.1:3000/hello`.

When app is deployed as a *Lambda function* it can be invoked thorugh AWS Lambda on web browser or also from AWS Cloud9 dev environment.

**Triggers** another type of trigger (instead of the API Gateway) is S3. When something is uploaded in the S3, this triggers the function.

![Screen Shot 2024-01-23 at 23 19 43](https://github.com/carlo088/iac_duke_course/assets/96287482/5d80f415-4db5-4951-9f95-92df21a72d5e)

## Serverless Data Pipeline
- AWS DynamoDB, create or use an existing table. Then add stuff in a newly created one or just visualize a know one. Lambda function will pull data from this DB and send it to SQS.
- AWS SQS to send messages (doesn't saturate, always works, can't blow up queue). Create queue and recieve/send messages. Will set trigger to when producer (Lambda that pulls from DynamoDB) sends a message and as batch size to process 1 message per time (and removes them from queue).
- AWS CloudWatch is the trigger. Fix a rate (for ex. once a minute). Also provides logs.
- AWS Lambda handler ('serverless_sentiment_lambda.py') will pull messages, find text in corresponding wikipedia pages and peform sentiment analysis
- AWS S3 recieves and holds what get sent from the lambda
