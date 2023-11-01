We will use:
1. Flask: to build, in python, microservices in web framework
2. Hugo: to generate static assets like .html files
3. AWS Code Pipeline is a CI/CD integrated in AWS framework

### Deploy Flask ML App on Azure
1. Access **Azure DevOps**
2. Configure project
- the course skips the part in which the project, along with the ```azure-pipeline.yml``` gets set up
4. Access **Pipeline** section -> by clicking on code, you will automatically be redirected on GitHub source code
5. A push in the repo triggers a new build in the DevOps Azure
6. By accessing web app on the server, the app is already running the new build

##### Adding a quality control gate
1. In project folder, access the ```azure-pipeline.yml```
2. Add the following
```
 - script:
      python -m pip install flake8
      flake8 .
      displayName: "Run lint tests"
```
or, if a Makefile has been configured:
```
- script:
      python -m venb antenv
      source antenv/bin/activate
      make install
      make lint
      displayName: "Run lint tests"
```
