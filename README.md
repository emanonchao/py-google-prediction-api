# py-google-prediction-api
Call Google Prediction API using Python 

#instructions

##Preequisites
- You must have a [Google Account](https://www.google.com/accounts/NewAccount),with a Google name and password.
- You must have a [Google Developers Console](https://console.developers.google.com) project with Google Prediction and Googe Cloud Storage activated.
- You must install all the libraries in library.txt(for example, pip install LIBRARY_NAME)

##Activate an API for your project
- Go to the [Google Developers Console](https://console.developers.google.com).
- Select a project, or create a new one.
- In the sidebar on the left, expand *APIs & auth*.
- Click *APIs*.
- In the displayed list of avaliable APIs, find the one you want to activate, and set its status to ON.

##Upload a dataset
- In your project dashboard, select *Cloud Storage > Storage browser*.
- You might be requested to enable billing for this feature.
- Click *New Bucket*, fill in as desired and upload your dataset.

##Get credentials
- In your project dashboard, select*APIs & auth > Credentials*.
- Click *Create New Client ID* and select the *Installed application* type. Next, look for your application's client ID and client secret in the relevant table.

##Run the file
- Open a terminal and go to the directory where your file is saved.
- Execute the following command:
```
python your_file_name  your_client_id  your_client_secret
```


#Examples
- Using Trained Models
``` python
#Get analysis of the model and the data the model was trained on
TrianedModel("PROJECT_ID", "MODEL_NAME").analyze()

#Delete a trained model
TrainedModel("PRJECT_ID", "MODEL_NAME).delete()

#Check training status of your model
TrianedModel("PORJECT_ID", "MODEL_NAME").get()

#Train a Prediction API model by an uploaded csv file
TrianedModel("PROJECT_ID", "MODEL_NAME").insert(storageDataLocation)

#Train a Prediction API model by specified dataset
#the format of training_instances should be like 
[
 {"output": "A String", #The generic output value - could be regression or classs label
 "csvInstance": [#The input features for this instance.
 "",
   ],
  },
 ]
TrainedModel("PROJECT_ID", "MODEL_NAME).insert(training_instances)

#List available models
TrainedModel("PROJECT_ID").list()

# Submit model id and request a prediction
#The format of csv_instances should be like ["A string", #The input features for this instance]
TrainedModel("PROJECT_ID", "MODEL_NAME").predict(csv_instances)

#Add new data to a trained model
TrainedModel("PROJECT_ID", "MODEL_NAME").update(output_value, csv_instances)


