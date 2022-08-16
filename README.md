# CapstoneProject_Anomaly_Detection_with_FL

## from March 2021 to June 2021  (USYD 2021 Semester 1)



### Federated Deep Auto-encoder Model
Deep Auto-encoder + Federated Learning

Local Model Architecture
![Local Deep Autoencoder](https://user-images.githubusercontent.com/80377806/124221430-2087e200-db43-11eb-9ec3-e9eede7ee880.png)

Federated Model Architecture
![FL-AE model](https://user-images.githubusercontent.com/80377806/124221443-24b3ff80-db43-11eb-80c3-ea09658e5f0f.png)


------------------------------------

### All Datasets

Original files can be downloaded from https://archive.ics.uci.edu/ml/datasets/detection_of_IoT_botnet_attacks_N_BaIoT or https://www.kaggle.com/datasets/mkashifn/nbaiot-dataset/download?datasetVersionNumber=1

Initial modified files store in https://drive.google.com/drive/folders/1hnKIBIIwI3564738E1NMosjVH7fT6BY1?usp=sharing


![number of data](https://user-images.githubusercontent.com/80377806/124221052-48c31100-db42-11eb-833f-203bd26471fc.png)


<img width="1235" alt="Data Distribution" src="https://user-images.githubusercontent.com/80377806/124221322-e9b1cc00-db42-11eb-9170-4e7af4d93298.png">
<img width="776" alt="Data attack distribution - pie" src="https://user-images.githubusercontent.com/80377806/124221381-0948f480-db43-11eb-994b-e22d82f0e6d1.png">




------------------------------------

### Anomaly Detection Steps:
1. convert 89 csv files to 9 csv files based on devices
2. load 9 csv files and library packages required
3. for each device, split benign and anomalous data
4. train model by using benign data only
5. calculate threshold to detect benign or anomalous
6. get detection results (1 - anomalous / 0 - benign)




------------------------------------

### Environment & Required Libraries/Packages
* Google Colab
* Pytorch
* pandas
* numpy
* matplotlib
* sklearn
* tqdm
* time



------------------------------------

### Main Modules
* Data pre-processing
* Retraining mechanism
* FedAvg / FedAvgM
* Random select partial devices for train
* Evaluation



------------------------------------

### To load datasets
  ```python
!pip install -U -q PyDrive
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials
# Authenticate and create the PyDrive client.
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

id = '1M3LKek2UCf9HXEieWLDpFHN8PSh7088u'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #1.csv')   # Device #1

id = '19H5gOya_F-DQbaOxyamV9nK3RuSjCgK2'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #2.csv')   # Device #2

id = '1lEd9Qq3q5vy9p4VQpWCGFcuxkrdq-9l6'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #3.csv')   # Device #3

id = '1HQ3txtS2WxzJrBlIhd3GaSVHwzcQEi61'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #4.csv')   # Device #4

id = '1fmzFIkM4FhAMa73uD36j7gHtdCF9-_QV'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #5.csv')   # Device #5

id = '1zk5riI0z3tiC_4OHgTYC7oWETihs65Lj'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #6.csv')   # Device #6

id = '1rJCtnpS_XeqALJ0-CJTrCBxsQwKYlZ30'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #7.csv')   # Device #7

id = '1Mg0A0Fcelu5nsgCgfS9evve4vHGoGha6'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #8.csv')   # Device #8

id = '152_3vZEkrTRrmSs0BpMNt6CQsSnHgO82'
downloaded = drive.CreateFile({'id':id}) 
downloaded.GetContentFile('Device #9.csv')   # Device #9

# add dataset links for other types of devices here....
  ```


  ```python
d1 = pd.read_csv('/content/Device #1.csv')
d2 = pd.read_csv('/content/Device #2.csv')
d3 = pd.read_csv('/content/Device #3.csv')
d4 = pd.read_csv('/content/Device #4.csv')
d5 = pd.read_csv('/content/Device #5.csv')
d6 = pd.read_csv('/content/Device #6.csv')
d7 = pd.read_csv('/content/Device #7.csv')
d8 = pd.read_csv('/content/Device #8.csv')
d9 = pd.read_csv('/content/Device #9.csv')
  ```
