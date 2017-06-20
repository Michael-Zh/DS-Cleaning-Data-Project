# Getting and Cleaning Data (Course 3) Project
## Data Science (JHU Coursera)

This project is for Data Science specialization on Coursera from JHU.

### This project requires the student:
1. A tidy data set as described below
2. A link to a Github repository with your script for performing the analysis
3. A code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md
4. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

### Specifically, the tidy data set refers to a R script called run_analysis.R that does the following:
1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

### Explanation on the R script run_analysis.R
Requirement 1: Merge two sets of data
 *Load the test and training data set, activities, and subjects labels
 *Merge the training and test data set
 *Merge the activities and subjects labels

Requirement 2: Extracts only the mean and std of each measurements
 *Load feature labels data
 *Locate feature labels with "mean" and "std"
 *Select needed columns

Requirement 3: Uses desriptive variable names
 *remove "()"，capitalize M and S, remove "-" in column names

Requirement 4: Uses descriptive activity names
 *Add activity and subject label
 *Use lower cases
 *Sub to descriptive activity names

Requirement 5: Create a data set with the average of each variable for each activity and each subject
 *Create a data frame structured as the expected result and name the columns
 *Loop by the subject and activity and calculate the column mean respectively, then fill in the designated cell in the data frame
 *write out the 2nd dataset
