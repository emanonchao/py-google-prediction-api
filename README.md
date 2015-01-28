# py-google-prediction-api
Call Google Prediction API using Python 

#instructions

##Prerequisites
- You must have a [Google Account](https://www.google.com/accounts/NewAccount),with a Google name and password.
- You must have a [Google Developers Console](https://console.developers.google.com) project with Google Prediction and Googe Cloud Storage activated.
- You must install all the libraries in library.txt(for example, pip install LIBRARY_NAME)

##Preparations

####Step1 Activate an API for your project
- Go to the [Google Developers Console](https://console.developers.google.com).
- Select a project, or create a new one.
- In the sidebar on the left, expand *APIs & auth*.
- Click *APIs*.
- In the displayed list of avaliable APIs, find the one you want to activate, and set its status to ON.

####Step2 Upload a dataset(optional)
- In your project dashboard, select *Cloud Storage > Storage browser*.
- You might be requested to enable billing for this feature.
- Click *New Bucket*, fill in as desired and upload your dataset.

####Step3 Get credentials
- In your project dashboard, select*APIs & auth > Credentials*.
- Click *Create New Client ID* and select the *Installed application* type. Next, look for your application's client ID and client secret in the relevant table.
- Add your application's client ID and client secret into *settings.py*

#Usage
- A simple example showing how to predict
``` python
import prediction

'''This example uses TrainedModel to do prediction.  
PROJECT_ID is the Project Number which is listed in the Overview tab in [Google Developers Console](https://console.developers.google.com).  
MODEL_NAME is the string id that will be used to reference the model, you can define it by yourself.'''
example = TrainedModel("PROJECT_ID", "MODEL_NAME")

'''Use a data file uploaded to the bucket to train your model
storageDataLocation is the Google Cloud Storage path where you uploaded your training data. '''
example.insert(storageDataLocation)

#Before doing prediction, you have to check the training status. You can't predict until the training process is done.
status = example.get()
while "DONE" not in status.["trainingStatus"]:
 status = example.get()
result = example.predict()
print result.["outputValue"]  #print the value of your prediction

#When you get new data later, you can also add them to a trained model
example.update(output_value, features)
```
There are two ways to train your model: one is to use a data file which is mentioned in the example above, another is to type in training data directly.
If you wanna use the latter one, and you can skip Step2 in Preparations. In this case, you should change the argument of insert function. Here is the example:
``` python
#Type in training data directly
#The format of training_data should be like
'''
[
 {"output": "A String", #The generic output value - could be regression or classs label
 "csvInstance": [#The input features for this instance.
 "",
   ],
  },
 ]
'''
example.insert(output_value, features)  
```


- Other functions
``` python
#Get analysis of the model and the data the model was trained on
TrianedModel("PROJECT_ID", "MODEL_NAME").analyze()

#Delete a trained model
TrainedModel("PRJECT_ID", "MODEL_NAME).delete()

#List available models
TrainedModel("PROJECT_ID").list()

#Train a Prediction API model by a dataset
TrainedModel("PROJECT_ID", "MODEL_NAME").insert(training_data)



