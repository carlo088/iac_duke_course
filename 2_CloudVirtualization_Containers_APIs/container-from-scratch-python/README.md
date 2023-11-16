#### container-from-scratch-python
This is building a container from scratch

### Build the Container Yourself and Push to Docker Hub

#### Build image
Dockerfile looks something like:
```
FROM python:3.7.3-stretch
# Working Directory
WORKDIR /app
# Copy source code to working directory
COPY . app.py /app/
RUN pip install --no-cache-dir --upgrade pip &&\
    pip install --no-cache-dir --trusted-host pypi.python.org -r requirements.txt
```

### List docker images
```docker image ls```

#### Run my newly built container
This command spins uo the app inside the container with the input as the flag --name. Note: this is running a remote image at noahgift/cloudapp, but one can also run a local one.

remote: ```docker pull noahgift/cloudapp:latest``` and
```docker run -it noahgift/cloudapp python app.py --name "Big John"```

local: ```docker run -it app python app.py --name "Big John"```

#### Build docker image
Then, one can build the container and push it to the Docker Hub. *Note:  You will need to change for your Docker Hub Repo*

```docker build --tag app .```

```docker push noahgift/duke102:tagname```


#### Push to Amazon ECR (Elastic Cloud Registry)

1.  Create ECR repository -> **all next instructions will be displayed**
2.  Copy command to log into newly created repo: ```aws ecr get-...```
3.  Build with ```docker build -t $NAME_OF_CONTAINER$ .```
4.  Follow tag command to tag the build ```docker tag ...```
5.  Push image to ECR with ```docker push ...```
6.  If I access new env, I can now ```docker pull ...``` the image

### More things Do

* Lint the code with Github Actions (see the Makefile)
* Automatically build the container after lint, and push to DockerHub or some other Container Registery



