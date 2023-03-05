**1. How did you approach the data pre-processing, data cleaning and data normalization? Attach the Queries used here.** [10 marks]

**2. How did you approach the problem statement? Explain briefly** [5 Marks]

**3.a. Give an example of similar data available on a larger scale and your recommended Hadoop architecture to maintain the data.** 
**3.b. What is your recommended maintenance activity for the architecture mentioned above** [5 Marks]


1. Approach to Data processing : 

In given dataset target is to predict the volume of passengers in train. Target variable contains three levels high(392), medium(360)and low(532),its looking like well distributed data without bias towards any level.

Data set contains 1284 observations and 19 variables. In that contains few missing values. Except mean_halt_times_destination all are categorical variables, so imputed all categorical variables with mode and continuous variables with mean.

Current_date and current_time both variables are presented as object type, converted these two variables into timestamp and extracted the date and hour features.

Source_name and destination_name presented with a number along with a string. String word is common in all observations,so removed the string word using regular expressions.

Country_code_sorce and country_code_destination variables contains four codes but there is no variance most of the observations code was same. And one more feature current_year also contains with no variance. So dropped the country_code features and current year feature.

Using longitude and latitude features calculated the distance between source station and destination station.

Aggregated the data on Train_name and current_day feature and created the features like how long train was travelled during the week day, average distance the train travelled on week day.

Aggregated the data on train_name and mean_halt_times and creted the features like total time how long the train was halt at source and destination and the average time aswell.

Later aggregated the data on source_name,destination,current_day  created the features like how many trains available between perticular source to destination, how many trains available between two stations week day wise,month wise and hour wise.
How many trains starts from a source staion day wise and hour wise and the same way created the features like how many trains reaching destination hour wise and day wise.

Finally created the dummies for current_day and is_weekend features and encoded the target lebels. 


2. Approach to Problem Statement :

Given problem is to predict the volume of passengers in train. Target is categorical variable that contains three levels. So Which is multi class classification problem. And the training data set contains Data set contains 1284 observations and 19 variables.

First I performed data cleaning and feature engeneering. Coming to model selection I Tried various models through cross validation like SVC,RandomForest,XGB,LGBM and Catboost. On given dataset LGB performed well. Performed parameter tuning and fitted the data on LGB model and predicted the target variable.


3.a. If the similar data available on a larger scale:

In hadoop we have parallerl processing and distributed computing features available. MapReduces performs the parallel processing, while HDFS performs the distributed computing.

	The fundamental framework of mapreduce is about breaking down the large chunks of datasets on parallel and distributed computing clusters. MapReduce identifies the closest cluster instead of trying to reach farther clusteres. JobTracker manages the identification of the location the data then it performs the orchestration of the tasks map and reduce. 
Recommended architecture would be mapreduce.

3.b.recommended maintenance activity :

Upgrading an HDFS and MapReduce cluster requires careful plannig. The most important consideration is the HDFS upgrade. If the layout version of filsesystem has changed, then the upgrade will automatically migrate the filesystem data and meta data to a format that is compatiable with the new version. As with any procedure that involves data migration, there is a risk of data loss, so we should be sure that both our data and meta data is backed up.





