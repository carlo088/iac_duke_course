**Containerize CLI Tool**: done through the Dockerfile and through a build.sh
`
FROM python:3.7
WORKDIR /app
COPY . app.py /app/
RUN pip install --upgrade pip &&\
    pip install --trusted-host pypi.python.org -r requirements.txt
`
`
#!/usr/bin/env bash
docker build --tag=clickecho .
docker run -it clickecho python app.py --name "Big John"
`
Docker image can then be deployed to a container registry such as AWS ECS and then run it from kubernetes and have it deployed.

# codespace-devops
This is a Python for DevOps Codespace Repo

## What it does

This is a basic cookbook for building command-line tools for the modern era

* Click CLI tool with full continuous integration
* Docker CLI 


## Additional Resources

* [Codespace Shell Command History](https://gist.github.com/noahgift/25cbeba2027e90396c650232a7f6bf60)
