# Code Book for Getting & Cleaning Data Project
## by Michael Zhang

This is a code book that describes the variables, the data, and any transformations or work that I performed to clean up the data.

### The data source
#### Quote from the original dataset
Human Activity Recognition Using Smartphones Dataset
Version 1.0

Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio, Luca Oneto.
Smartlab - Non Linear Complex Systems Laboratory
DITEN - Universit‡ degli Studi di Genova.
Via Opera Pia 11A, I-16145, Genoa, Italy.
activityrecognition@smartlab.ws
www.smartlab.ws

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.
#### Note from Michael:
I used following original files to create this project:
* 'features.txt': List of all features.
* 'activity_labels.txt': Links the class labels with their activity name.
* 'train/X_train.txt': Training set.
* 'train/y_train.txt': Training labels.
* 'test/X_test.txt': Test set.
* 'test/y_test.txt': Test labels.
* 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample in training group. Its range is from 1 to 30. 
* 'test/subject_test.txt': Each row identifies the subject who performed the activity for each window sample in test group. Its range is from 1 to 30. 

### The transformations
Based on the original data set:
1. I first merged the training and test data to one data set, as well as the activity and subject labels 
2. Then I selected only "mean" and "standard deviation" features among all variables (these calculations were done in the original data set, I just selected the correspondent columns) to create the first data set "Merged_dataset.txt."
3. Based on the result of the second step, I calculated the average of each variable by each activity and each subject, creating a new dataset called "Mean_dataset.txt."

### The variables

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
* 'mean' is used to denote the mean of a certain feature.
* 'std' is used to denote the standard deviation of a certain feature.
* 'XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

Additionally:
* 'Activitiy' denotes the acitivity from which the signal is devrived.
* 'Subject' denotes the subject who performed certain activity.

List of all variables
 [1] "Activity"                 "Subject"                  "tBodyAccMeanX"           
 [4] "tBodyAccMeanY"            "tBodyAccMeanZ"            "tBodyAccStdX"            
 [7] "tBodyAccStdY"             "tBodyAccStdZ"             "tGravityAccMeanX"        
[10] "tGravityAccMeanY"         "tGravityAccMeanZ"         "tGravityAccStdX"         
[13] "tGravityAccStdY"          "tGravityAccStdZ"          "tBodyAccJerkMeanX"       
[16] "tBodyAccJerkMeanY"        "tBodyAccJerkMeanZ"        "tBodyAccJerkStdX"        
[19] "tBodyAccJerkStdY"         "tBodyAccJerkStdZ"         "tBodyGyroMeanX"          
[22] "tBodyGyroMeanY"           "tBodyGyroMeanZ"           "tBodyGyroStdX"           
[25] "tBodyGyroStdY"            "tBodyGyroStdZ"            "tBodyGyroJerkMeanX"      
[28] "tBodyGyroJerkMeanY"       "tBodyGyroJerkMeanZ"       "tBodyGyroJerkStdX"       
[31] "tBodyGyroJerkStdY"        "tBodyGyroJerkStdZ"        "tBodyAccMagMean"         
[34] "tBodyAccMagStd"           "tGravityAccMagMean"       "tGravityAccMagStd"       
[37] "tBodyAccJerkMagMean"      "tBodyAccJerkMagStd"       "tBodyGyroMagMean"        
[40] "tBodyGyroMagStd"          "tBodyGyroJerkMagMean"     "tBodyGyroJerkMagStd"     
[43] "fBodyAccMeanX"            "fBodyAccMeanY"            "fBodyAccMeanZ"           
[46] "fBodyAccStdX"             "fBodyAccStdY"             "fBodyAccStdZ"            
[49] "fBodyAccJerkMeanX"        "fBodyAccJerkMeanY"        "fBodyAccJerkMeanZ"       
[52] "fBodyAccJerkStdX"         "fBodyAccJerkStdY"         "fBodyAccJerkStdZ"        
[55] "fBodyGyroMeanX"           "fBodyGyroMeanY"           "fBodyGyroMeanZ"          
[58] "fBodyGyroStdX"            "fBodyGyroStdY"            "fBodyGyroStdZ"           
[61] "fBodyAccMagMean"          "fBodyAccMagStd"           "fBodyBodyAccJerkMagMean"

[64] "fBodyBodyAccJerkMagStd"   "fBodyBodyGyroMagMean"     "fBodyBodyGyroMagStd"     
[67] "fBodyBodyGyroJerkMagMean" "fBodyBodyGyroJerkMagStd" 
