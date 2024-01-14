### Microservices ``
In general, a DevOps practice. Main advantages: serverless (code runs without provisioning servers).
Small, autonomous, specialized, high degree of reliability.
Where can one run a Microservice? In a container or on a cloud service such as AWS Lambda: a serverless compute service that runs your code in response to events

*Flask* Very common, it **maps a python function to a URL**, that's why basic method is @route. 
*API* to define interactions between services.
*JSON* to interchange data.

Deploying on Azure: once Flask app is ready, push it to azure with `az webapp up -sku F1 helloflask`.
Now app is on public website and can be accesseed by anyone! From now only, for any local change in source code, just update with `az webapp up`.
