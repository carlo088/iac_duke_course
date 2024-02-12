## MLOps
DevOps best practices applied to ML.

Saving and reloading models: 
`joblib.dump(model, 'model_prediction.joblib')` and
`joblib.load('model_prediction.joblib')`
Dumb method let's you persist an arbitrary Python object into one file.

### Edge ML
To deploy ML on edge devices, due to latency requirements.

**SDK**: software development kit,they put everything you need to develop and run software in one place. **OONX** is a format to save, store and retrieve ML models ex: `YOLO_model.mlmodel`.

#### Edge ML in AWS

**AWS Deeplens**: workflow to use a Deeplens device, which has a deep-learning enable camera integrated. Many off the shlef, already deployable projects. The camera feeds video, lambda function makes prediction through a pre-trained resnet network and sends the result to an UI. Also gives access to the device logs: probabilities of object detection. Also lets you look into lambda function itself, in case one wanted to tweak something.

### APIs

An example is **boto3**, a python library to create, configure, and manage AWS services.

**AWS Comprehend** is an API for NLP. The UI let's one submit a text and the service will extract a summmary and other insights. It can also be used through the API. After having `pip install boto3', run `comprehend = boto3.client('comprehend')'. This let's one call for example `comprehend.detect_key_phrases(Text=text, languageCode='en')`.

**AWS Rekognition** let's one do Computer Vision, for applications such as Obejct Detection. Also available thorugh UI or API: `rekognition = boto3.client('rekognition')` and `response = boto3.client.detect_labels(Image=image).

**Building a Web Service:** build a Flask app, and deploy on a Cloud serivce (such as AWS Beanstalk). And how does one pull data from users? Generally data is recieved from user through a *GET* and then data get sent through a *POST*, where both services rely on the HTTP protocol. **Flask** will have a route that pulls input, processes.

Building a ML application: 
- Start from security, run authenticaion with AWS Cognito
- The app will live in the Cloud and deliver predictions on input images
- Use CD for deployable code, Automatic Development, Testing and Linting
- Add monitoring a logging for issues
- Postman to test the web APIs
- Use a PaaS like AWS Beanstalk to garantee Elastic service
- Store code in a deployable state in GitHub, also through nightly tests with tools such as Loader.io or Locust
- 
