### Cloud Computing

#### Static S3 Website
Store a index.html file in a S3 bucket (which is, essentially, a folder) where your website will live. Then enable website.
1. Create a ```index.html```
2. Create a S3 bucket, give it a name: hellocloud4data
3. Access bucket from aws console and enable static website
4. Upload ```index.html``` through the console
5. Access (worldwide) at the provided url

#### Serverless Website on Lambda
Lambda: lets you store a python function that will trigger at specific events.
1. Create new lambda function, giving it a name
2. Select runtime: python
3. Select function trigger: API Gateway
4. It will create a scaffold in your repo
5. Insert your logic in the ```lambda_function```
6. The run, but: Run API Gateway local
7. Then deploy
Difference w.r.t. earlier: earlier we had a *static* website, while now we have a *serverless* one that works with a trigger.

#### Building a Website on a EC2 VM
