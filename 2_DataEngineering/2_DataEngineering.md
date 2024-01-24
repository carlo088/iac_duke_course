## Data Engineering
Building Pipelines to move and store data to have it ready for analysis.
*Batch* data is delivered in batches while *Streaming* data is continuosly delivered.

#### AWS CodeGuru
First step is to "Associate Repo". Use repo from GitHub.
CodeGuru reviews code and provides reccomendations.
Other interesting tool: **codeclimate**.

#### AWS CodeBuild
Similar to GitHub Actions, to test code in AWS systems.

#### AWS Lambda
Function as a service. Holds the python function that has all your logics. **Chech awslamba folder for more on this topic**


## Data Governance (Security)
Engineering security for handling data. First thing: create users, groups and policies -> AWS IAM

#### AWS AIM
Define username and select what they have access to. Then create group and policy (ex: read from an S3) and security levels. Console provides all groups and users and permissions. Also permissions for accessing a Lambda API. Conclusion AIM let's you associate roles users with polciies and therefore build your security policy.

Service provides security for mangement of code and data, in general. Security is done by both client and AWS itself. AWS provides accessible cost, performance, security. Also provides logs on who does what and helping in troubleshooting.

Encryption: *transit* to encrypt all communications with server, *rest* instead stores encrypted data and *keys* are used to decrypt, so the keys have to be guarded.





TIP: ```df -h``` print to CLI the available space
