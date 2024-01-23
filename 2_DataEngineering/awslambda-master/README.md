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
