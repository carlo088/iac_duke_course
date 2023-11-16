#### Kubernetes
What is K8s: container orchestration service.

Kuberntes manages a Cluster. Clusters are made by Nodes that contain Pods, which can contain one or more containers.
![Screen Shot 2023-11-16 at 22 49 31](https://github.com/carlo088/iac_duke_course/assets/96287482/a1e52e7b-dcb8-4b94-9c7d-9832942a310c)
![Screen Shot 2023-11-16 at 22 55 39](https://github.com/carlo088/iac_duke_course/assets/96287482/482ad8a8-8710-4ad4-949d-b6bda077f039)

#### Basic Example
Basic example of a ```yaml``` file deploying a K8s cluster.
Here we are just fetching 1 image and asking to have the service at port 80.
```
version: '3.3'

services:
  web:
    image: dockersamples/k8s-wordsmith-web
    ports:
    - "80:80"

words:
  image: dockersamples/k8s-wordsmith-api
  deploy:
    replicas: 5
    endpoint_mode: dnsrr
    resources:
      limits:
        memory: 50M
      reservations:
        memory: 50M
db:
  image: dockersamples/k8s-wordsmith-db
```
Can be deployed with ```docker stack deploy ...```

##### Autoscaling is Kubernetes killer feature

### Deploy App to GKE (Google Kubernetes Engine)
1. Setup GKE
2. Run ```gcloud container cluster create ...```
3. Once the service has been provisioned, I can run app
4. Run by ```kubectl create deployment ... $point to container$```
5. Execute by ```kubectl espose deployment ... --port $PORT_NUMBER$```
6. Overview of situation with ```kubectl get service```, once the service is ready, I can access the service at the port requested.
7. Lastly, I can delete cluster with ```gcloud container cluster delete ...```

#### run_kubernetes.sh
Put all in a single bash script.
Set a docker path for the local deployment.
```kubectl``` is as usual the K8s API.
Run app and forward port to the host.
```kubectl get pods``` to list available pods.
Run command with ```./run_kubernetes.sh```
```
#!/usr/bin/env bash

dockerpath="noahgift/flasksklearn"

# Run in Docker Hub container with kubernetes
kubectl run flaskskearlndemo\
    --generator=run-pod/v1\
    --image=$dockerpath\
    --port=80 --labels app=flaskskearlndemo

# List kubernetes pods
kubectl get pods

# Forward the container port to host
kubectl port-forward flaskskearlndemo 8000:80
```

### Deploying a Kubernetes Python Flask App
Assets in Repo:

Makefile:  Builds project

Dockerfile:  Container configuration

app.py:  Flask app

kube-hello-change.yaml: Kubernetes YAML Config


1. Build and run Docker container:
2. ```docker build -t flask-change:latest .``` or ```make build```
3. then ``` docker run -p 8080:8080 flask-change``` or ```make run```
4. In a separate terminal invoke the web service via curl: ```make invoke``` which has the same command ```curl http://127.0.0.1:8080/change/1/34```
5. Run the application in Kubernetes using the following command which tells Kubernetes to setup the load balanced service and run it:
```kubectl apply -f kube-hello-change.yaml or run make run-kube```
