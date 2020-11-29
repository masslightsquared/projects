# COVID-19 Time Series Data

## Motivation
In this project we use regression models to analyze the COVID-19 confirmed cases dataset published by the Center for Systems Science and Engineering (CSSE) at Johns Hopkins University. 

## Step 1: Read the Data
We first read in the dataset using Pandas's read_csv() function.
```
$ import pandas as pd
$ data = pd.read_csv('time_series_covid_19_confirmed.csv') 
```
The dataset's features are Province/State, Country/Region, Latititude, Longitude and the time series of confirmed cases from January 22, 2020 to August 29, 2020. Each row of the dataset can be conceptualized as representing a Country or Region, where we are given the geographical location and number of confirmed cases within for that region. There are 266 countries and each sample (country) has 225 features.

## Step 2: Convert the Tabular Data
To train our regression models, we will need to convert the tabular data to format {X,Y}, where X = {Longitude, Latitude, Date} and Y = {#infected}.
```
#Finding the date indices
$ import matplotlib.pyplot as plt
$ data_row=data_new.sum(axis=0)
$ days=range(0,data_row.shape[0])
$ days_mat=matlib.repmat(np.array(days),data_new.shape[0],1)
$ print(days_mat.shape)
```


```
$ #Lets create data X-{X1,X2,X3}, where X1=lat, X2=long, X3=date, Y=#affected
$ X=np.zeros((days_mat.shape[0]*days_mat.shape[1],3))
$ Y=np.zeros((days_mat.shape[0]*days_mat.shape[1],1))
$ lat_long=np.array(data.iloc[:,2:4])
$ data_new=np.array(data_new)
$ for r in range(days_mat.shape[0]): #all locations
   X[r*days_mat.shape[1]:r*days_mat.shape[1]+days_mat.shape[1],0]=lat_long[r,0]*np.ones((days_mat.shape[1],)) #setting Latitude
   X[r*days_mat.shape[1]:r*days_mat.shape[1]+days_mat.shape[1],1]=lat_long[r,1]*np.ones((days_mat.shape[1],)) #setting Longitude
   X[r*days_mat.shape[1]:r*days_mat.shape[1]+days_mat.shape[1],2]=np.reshape(days,(days_mat.shape[1],)) #setting the date
   Y[r*days_mat.shape[1]:r*days_mat.shape[1]+days_mat.shape[1]]=np.reshape(data_new[r,:],((days_mat.shape[1],1)))
```

Optionally you can set `DEBUG=1` to also print statistics to `stdout`. `CARBON_PREFIX` can also be set to override the default namespace (`nagios.problems`).

```
$ DEBUG=1 bundle exec ruby ledbetter.rb
nagios.problems.all 41 1359170720
nagios.problems.critical 27 1359170720
nagios.problems.warning 12 1359170720
nagios.problems.unknown 2 1359170720
nagios.problems.servicegroups.apache 0 1359170720
nagios.problems.servicegroups.backups 3 1359170720
nagios.problems.servicegroups.dns 0 1359170720
nagios.problems.servicegroups.mysql 1 1359170720
...
```

## License 

Ledbetter is distributed under the MIT license.



