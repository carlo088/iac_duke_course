Objective: Container base, sourced control repository and push the code to a container hub. All of this while applying best DevOps principles.

#### **For more on how to build and push a docker image to AWS ECR, look into README of the project in this folder**

#### Containers
1. Build Cloud-native applications
2. DevOps best practice
3. Microservices
4. Include runtime and code
5. Fast to launch

### Docker
![alt text](https://user-images.githubusercontent.com/58792/73697366-5d307f00-46ac-11ea-9f85-529a9e3c4f42.png)
Docker Desktop for local workflow, GUI to monitor running containers.

Docker Hub for public/private repos (docker containers). It stores images: for example, for most projects, one would first of all pull latest python image to begin with.

Example: pulling a Jupyter environment. By just running  ```docker pull jupyter/datascience-notebook``` one can access a complete and complex jupyter setup.
Secondly, run the environment with ```docker run -p 8888:8888 jupyter/scipy-notebook:latest``` (where ```-p``` is used to map the port).
Now, access jupyter environment from the local host at port 8888.


More can be found at:
https://noahgift.github.io/cloud-data-analysis-at-scale/topics/docker-format-containers
