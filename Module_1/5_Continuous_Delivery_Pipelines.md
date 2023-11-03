We will use:
1. Flask: to build, in python, microservices in web framework
2. Hugo: to generate static assets like .html files
3. AWS Code Pipeline is a CI/CD integrated in AWS framework

### Deploy Flask ML App on Azure
1. Access **Azure DevOps**
2. Configure project
*the course skips the part in which the project, along with the ```azure-pipeline.yml``` gets set up. Scroll down for complete ```azure-pipeline.yml```*
4. Access **Pipeline** section and run app service
5. Now by clicking on code, you will automatically be redirected on GitHub source code (remember that Azure Pipelines has to be enabled in GitHub repo)
6. A push in the repo triggers a new build in the DevOps Azure
7. By accessing web app on the server, the app is already running the new build

Link to repo: https://github.com/noahgift/flask-ml-azure-serverless

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

### Setup Hugo Website
Building static website with Hugo

https://d3c33hcgiwev3.cloudfront.net/vTjJyofrQS24ycqH6zEt4w_a72aad10ea7c4f5f9f10f63d8df4801f_Continuous-Delivery-for-Hugo-Static-Site-from-Zero.pdf?Expires=1699142400&Signature=j5~sxFELCx4eQZ~yHSMqQuKbTAWBtMhpaX~fw9PwLm3VJ8pJlivbXKE~ksAfOMJIaaa0Z4x7Q-WJICUXU7eeR~o7ewp8MvCBptFOH3ofbQ5vonxMwNtgJY-N8iebE08NT-Aw5f5ZP~Ztj0swJBjl5TdjsEwKAW0JDlkKyy6FYTY_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A

#### AWS CodeBuild
Automatically build code when GitHub repo is updated. In this case we have a Hugo website living in a S3 bucket. 
1. Create build project and link it to repo
2. Tell CodeBuild to build code according to a ```buildspec.yml```
3. Build the ```buildspec.yml``` and tell CodeBuild where to look for it. It will look something like:
```
version: 0.1

environment_variables:
  plaintext:
    HUGO_VERSION: "0.42"

phases:
  install:
    commands:
      - cd /tmp
      - wget https://github.com/gohugoio/hugo/releases/\
      download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
      - tar -xzf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
      - mv hugo /usr/bin/hugo
      - cd -
      - rm -rf /tmp/*
  build:
    commands:
      - rm -rf public
      - hugo
  post_build:
    commands:
      - aws s3 sync public/ s3://<yourwebsite>.com/ --region us-west-2 --delete
      - aws s3 cp s3://<yourwebsite>.com/\
      s3://<yourwebsite>.com/ --metadata-directive REPLACE \
        --cache-control 'max-age=604800' --recursive
      - aws cloudfront create-invalidation --distribution-id=<YOURID> --paths '/*'
      - echo Build completed on `date`
```
4. GitHub repo and CodeBuild are connected

##### azure-pipeline.yml
```
# Python to Linux Web App on Azure
# Build your Python project and deploy it to Azure as a Linux Web App.
# Change python version to one thats appropriate for your application.
# https://docs.microsoft.com/azure/devops/pipelines/languages/python

trigger:
- master

variables:
  # Azure Resource Manager connection created during pipeline creation
  azureServiceConnectionId: 'df9170e4-12ed-498f-93e9-79c1e9b9bd59'
  
  # Web app name
  webAppName: 'flask-ml-service'

  # Agent VM image name
  vmImageName: 'ubuntu-latest'

  # Environment name
  environmentName: 'flask-ml-service'

  # Project root folder. Point to the folder containing manage.py file.
  projectRoot: $(System.DefaultWorkingDirectory)
  
  # Python version: 3.7
  pythonVersion: '3.7'

stages:
- stage: Build
  displayName: Build stage
  jobs:
  - job: BuildJob
    pool:
      vmImage: $(vmImageName)
    steps:
    - task: UsePythonVersion@0
      inputs:
        versionSpec: '$(pythonVersion)'
      displayName: 'Use Python $(pythonVersion)'
    
    - script: |
        python -m venv antenv
        source antenv/bin/activate
        python -m pip install --upgrade pip
        pip install setup
        pip install -r requirements.txt
      workingDirectory: $(projectRoot)

    - script: |
        python -m venv antenv
        source antenv/bin/activate
        make install
        make lint
      workingDirectory: $(projectRoot)
      displayName: 'Run lint tests'

    - task: ArchiveFiles@2
      displayName: 'Archive files'
      inputs:
        rootFolderOrFile: '$(projectRoot)'
        includeRootFolder: false
        archiveType: zip
        archiveFile: $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
        replaceExistingArchive: true

    - upload: $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
      displayName: 'Upload package'
      artifact: drop

- stage: Deploy
  displayName: 'Deploy Web App'
  dependsOn: Build
  condition: succeeded()
  jobs:
  - deployment: DeploymentJob
    pool:
      vmImage: $(vmImageName)
    environment: $(environmentName)
    strategy:
      runOnce:
        deploy:
          steps:
          
          - task: UsePythonVersion@0
            inputs:
              versionSpec: '$(pythonVersion)'
            displayName: 'Use Python version'

          - task: AzureWebApp@1
            displayName: 'Deploy Azure Web App : flask-ml-service'
            inputs:
              azureSubscription: $(azureServiceConnectionId)
              appName: $(webAppName)
              package: $(Pipeline.Workspace)/drop/$(Build.BuildId).zip
```
