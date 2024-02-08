## AutoML
Best practices to automatize a ML pipeline. Have some data and a Cloud Env that runs the model on the new data.
Then model is ready to be deployed or used.
**Apple Create ML**: workflow to ingest, train and evaluate. This is a No Code/Low Code approach.
Guides you in generating folder with data correctly stored (thing about categories in a CV classification task).
**GCP AutoML**: provides a similar framework.
**AWS Comprehend**: similar workflow, supports MLP. Feed a text as input, and the workflow will provide analysis.
Statistics on words in text, sentiment analysis.
**AWS Rekognition**: provides similar framework, but for images.
**AWS Machine Learning**: allows to ingest tabular data. Then processes data and enables prediction features.
Select one column of the tabular data to be predicted, and AWS will generate a model to make a prediction.
You've built a ML model without writing any code!
**Azure Machine Learning** provides similar tools.

### Ludwig AutoML
Open source, code-free  toolbox for AutoML. User only has to put up a configuration file, telling task and where data is.
Example: `ludwig experiment --dataset $YOUR_DATASET --config_file config.yaml`

### Cloud AutoML
Guideline to build a complete ML workflow in the cloud. For example Azure Machine Learning Studio provides tons of different tools.
Steps:
1. generate dataset: easy way to go can be generate one (upload) from "Open Datasets" (an existing dataset). Azure gives option for importing and provides overviews all along. Note: alomg whole process, the workflow writes documentation.
2. automated ML Run: select data, select target column, select compute cluster (it's a cluster of VMs, which has to be defined like an EC2 istance) and number of cores, task (such as classification). Then execute Run.
3. deploy: after having analyzed results with graphs an metrics, Deploy. Select service such as a Container istance or a Kubernetes service, also select authentication. This deploys model, meaning that anyone can access it and use it, meaning that you'll get billed!
4. endpoints: Azure also provides feature to make tests, check metrics, logs 

