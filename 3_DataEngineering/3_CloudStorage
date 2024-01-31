## Cloud Storage

**ETL**: extract, transform, load (referred to data).

**AWS Glue** is a serverless ETL that intgerates with **Amazon Athena** that we will use to query.
Glue used to crawl data: add table and point it to a S3 bucket and "Data stores" as source type.
Then *run the crawler*: it will go inside S3 and read everything.
At the end, will create a table with the information on the data.
From AWS Console, one can directly change the schema (the metadata) of what was just crawled.

Then *query data*: this leads to Athena UI. Connect to S3, look at metadata from Glue and query directly the S3 from the UI.
Query results can also be pointed to another S3.
These tools make the ETL pipeline much faster and code-free!

### Cloud Databases
From Console, go to **RDS** -> "Create Database" (use RDS for fully managed DBs).

**AWS Aurora**: to spin up a SQL and serverless option.

**AWS DynamoDB**: one may prefer this to a SQL database. It's like and Excel database.
Made up of key-value pairs. The tools like *boto* can talk to it.

**AWS Redshift**: from Console, create cluster, load data from S3 and query the data in Redshift.
Use Case: use Redshift to continuosly query a DB and produce reports.

Why spin up an "entire" cluster? Assumption is that data is big, so one needs such a thing as a cluster.
So one has to select which type of EC2 cluster and numbers of nodes. Along with creating cluster, IAM roles have to be defined.
So next step is to create a security group for users to access the Redshift.
Then select "modify" to configure cluster to have access to security group.

Then access "Query editor" and build a query. Then "run" creates the *schema* or table.
One can build multiple schemas which will in turn create multiple tables.


### Cloud Storage
Major advantage is scalability. **Data Lake** is where once can build ML pipelines, have storage, host webs...
It's scalable, realiable and solid. 11 9's reliability (0.nine 9s).
AWS offers: object storage (files, images, ecc.), Databases (such as DynamoDB, or a graph database) and ETL systems (such as Glue) and EC2 (in general).

**AWS S3**: go to Console -> S3. Create unique bucket, default settings, private and not on a website.
Then one can upload stuff. Then from cli, one can sync bucket: `aws s3 sync s3:$NAME_OF_BUCKET .`.
This brings in CWD what's inside the bucket. Then, same command uploads data from CWD to bucket: `aws s3 sync . s3:$NAME_OF_BUCKET`



