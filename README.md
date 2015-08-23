## Course Project - Getting and Cleaning Data

# Step One: Merge training and test sets to create one data set.
tidy <- function() {
  #install and load helper libraries

  library(dplyr)
  library(stringr)

  #read test table from files imported into project
  XTest <- read.table("UCI-HAR-Dataset/test/X_test.txt")
  #read train table
  XTrain <- read.table("UCI-HAR-Dataset/train/X_train.txt")

  #merge sets by adding the rows of the training data to the test data
  combinedSets <- rbind(XTest, XTrain)


  # Step Two: Extract measurements on the mean and standard deviation for each measurement.
  # Collect the feature names and apply to combined set to find means & standard deviations

  features <- read.table("UCI-HAR-Dataset/features.txt")

  # find all columns containing the string "mean"
  means <- features %>% filter(str_detect(V2, "mean"))

  # find all columns containing the string "std
  stds <- features %>% filter(str_detect(V2, "std"))

  #subset data in the combinedSets with the row numbers extracted above

  meansSets <- combinedSets[,means$V1]
  stdSets <- combinedSets[,stds$V1]


}
# Use descriptive activity names to name the activities in the data set

activities <- read.table("UCI-HAR-Dataset/activity_labels.txt")
YTest <- read.table("UCI-HAR-Dataset/test/y_test.txt")
YTrain <- read.table("UCI-HAR-Dataset/train/y_train.txt")


# Label data set with descriptive variable names.


# Create second, independent tidy data set w/average of each variable for each activity
# and each subject.

# get subject information
subTest <- read.table("UCI-HAR-Dataset/test/subject_test.txt")
subTrain <- read.table("UCI-HAR-Dataset/train/subject_train.txt")
