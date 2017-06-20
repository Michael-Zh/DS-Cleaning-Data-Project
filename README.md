# Getting and Cleaning Data (Course 3) Project
## Data Science (JHU Coursera)

This project is for Data Science specialization on Coursera from JHU.

### This project requires the student:
1.A tidy data set as described below
2.A link to a Github repository with your script for performing the analysis
3.A code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md
4.You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

### Specifically, the tidy data set refers to a R script called run_analysis.R that does the following:
1.Merges the training and the test sets to create one data set.
2.Extracts only the measurements on the mean and standard deviation for each measurement.
3.Uses descriptive activity names to name the activities in the data set
4.Appropriately labels the data set with descriptive variable names.
5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

### Explanation on the R script run_analysis.R
1.Requirement 1: Merge two sets of data
  *Load the test data set, activities, and subjects labels
testData <- read.table("X_test.txt")
testActLabel <- read.table("y_test.txt")
testSubLabel <- read.table("subject_test.txt")

## Set the working directory of training data set
setwd("~/Documents/Data Science/C3-Cleaning-data/UCI HAR Dataset/train")

## Load the training data set, activities, and subjects labels
trainData <- read.table("X_train.txt")
trainActLabel <- read.table("y_train.txt")
trainSubLabel <- read.table("subject_train.txt")

## Merge the training and test data set
fullData <- rbind(trainData, testData)

## Merge the activities and subjects labels
fullActLabel <- rbind(trainActLabel, testActLabel)
names(fullActLabel) <- "Activity"
fullSubLabel <- rbind(trainSubLabel, testSubLabel)
names(fullSubLabel) <- "Subject"

## =================

## Requirement 2: Extracts only the mean and std of each measurements

## Load feature labels data
setwd("~/Documents/Data Science/C3-Cleaning-data/UCI HAR Dataset")
featureLabel <- read.table("features.txt")

## Locate feature labels with "mean" and "std"
temp <- grepl("mean\\(\\)|std\\(\\)", featureLabel$V2)

## Select needed columns
fullData <- fullData[,temp]

## =================

## Requirement 3: Uses desriptive variable names

names(fullData) <- gsub("\\(\\)", "", featureLabel[temp, 2]) # remove "()"
names(fullData) <- gsub("mean", "Mean", names(fullData)) # capitalize M
names(fullData) <- gsub("std", "Std", names(fullData)) # capitalize S
names(fullData) <- gsub("-", "", names(fullData)) # remove "-" in column names

## Save a copy of variable labels
varLabel <- names(fullData)

## =================

## Requirement 4: Uses descriptive activity names

## Add activity and subject label
fullData <- cbind(fullActLabel,fullSubLabel,fullData)

## Use lower cases
activity <- read.table("activity_labels.txt")
activity[, 2] <- tolower(activity[, 2])

## Sub to descriptive activity names
fullData[,"Activity"] <- activity[fullData[,"Activity"],2]

write.table(fullData, "Merged_dataset.txt") # write out the 1st dataset

## =================

## Requirement 5: Create a data set with the average of each variable for each activity and each subject

subjectLen <- length(table(fullSubLabel)) # 30
activityLen <- dim(activity)[1] # 6
columnLen <- length(fullData)
result <- matrix(NA, nrow=subjectLen*activityLen, ncol=columnLen)
result <- as.data.frame(result)
colnames(result) <- colnames(fullData)
row <- 1
for(i in 1:subjectLen) {
        for(j in 1:activityLen) {
                result[row, 2] <- sort(unique(fullSubLabel)[, 1])[i]
                result[row, 1] <- activity[j, 2]
                b1 <- i == fullData$Subject
                b2 <- activity[j, 2] == fullData$Activity
                result[row, 3:columnLen] <- colMeans(fullData[b1&b2, 3:columnLen])
                row <- row + 1
        }
}
head(result)
write.table(result, "Mean_dataset.txt") # write out the 2nd dataset
