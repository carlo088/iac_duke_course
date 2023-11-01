### Cloud Computing
Most of this has been done from a AWS *Cloud9* shell

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

#### Building a Website on a AWS EC2 VM
Now, do the building on a EC2 VM.
1. ssh into VM
2. Move into ```cd /var/www/html```
3. Create and write the ```index.html```

#### Building a Website with AWS Beanstalk
Provides load balancer between different VMs. Just on a CLI, everything is handled behind the scenes.
1. Install the ```EB CLI``` by following instructions - now run commands with ```eb```
2. Create a ```eb-flask``` dir to store flask app
3. To get and store requirements ```pip freeze > requirements.txt```
4. Create ```application.py``` with source code for the app
5. Create ```.ebignore``` and put the ```virt``` (virtual environment) inside to avoid deploying it
6. Then ```eb init -p python-3.6 flask-cloud-data```
7. To deploy ```eb create flask-cloud-dataenv```
8. Go back to AWS console and find link with the app
9. To clean up and avoid getting billed for this website ```eb terminate flask-cloud-dataenv```
