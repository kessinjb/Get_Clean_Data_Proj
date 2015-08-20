---
title: "README"
author: "john_kessing"
date: "Wednesday, August 19, 2015"
output: html_document
---

This is the README document that contains my scripts along with descriptions about how I worked thru:
Getting and Cleaning Data course project.

The first thing I did was perform the basic pre-process steps to prepare my environment.  After that I simply loaded the files leveraging the simplest process possible.  See process below:

```{r}
## loading data
# sets working directory
setwd("C:/Users/jbkessin/Documents/Get_Data_Proj")

# load dplyr
library(dplyr)

# read in first train file
x_train <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/train/X_train.txt"
           , header = FALSE)
# read in train labels, this file has code for which activity generated data in x_train
y_train <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/train/y_train.txt"
                      , header = FALSE)
# read in subject_train, this file contains which volunteer generated data
subject_train <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/train/subject_train.txt"
                      , header = FALSE)
# read in activity labels, this file has labels for what each activity is, joins to train labels
activity_labels <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/activity_labels.txt"
                      , header = FALSE)
# read in feature labels, this file lists the column names of all of the variables in train/test data sets
features <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/features.txt"
                              , header = FALSE)
# read in first test file
X_test <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/test/X_test.txt"
                      , header = FALSE)
# read in test labels, this file has code for which activity generated data in x_train
y_test <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/test/y_test.txt"
                      , header = FALSE)
# read in subject_test, this file contains which volunteer generated data
subject_test <- read.table("C:/Users/jbkessin/Documents/Get_Data_Proj/UCI HAR Dataset/test/subject_test.txt"
                            , header = FALSE)

```

My next steps was to combine the two main data sets and clean up the file that contains the names for all variables in the data set.  I leveraged the gsub function to remove extra characters and fully attribute some abbreviations.

I then added the column names to the main file and removed duplicate columns.

```{r}

## Combine datasets of test and training result data
train_test <- bind_rows(x_train, X_test)

# Clean-up features names
features1 <- gsub("[[:punct:]]", "", features$V2)
features1 <- gsub("Acc", "accelerometer", features1)
features1 <- gsub("Gyro", "gyroscope", features1)
features1 <- gsub("Mag", "magnitude", features1)
features1 <- gsub("BodyBody", "body", features1)

## this code adds attributes to train data set
# insert names into train_test file
col_names <-  as.vector(features1)
colnames(train_test) <- col_names
train_test <- tbl_df(train_test)
# remove duplicate column names due to issues later found
train_test1 <-  train_test[ ,!duplicated(colnames(train_test))]

```

Next, I pair down the column list to only columns containing mean or standard deviation measures.  Then I add the attribute information.  Activity information is binded together, then I join to get the descriptions.  Subject attribute is binded.  End result is a fully attributed file with all records, ready for final step.

```{r}
## Select only measures related to mean and std dev, selected things with ()
mean_sd <- bind_cols(select(train_test1, contains("mean")),select(train_test1, contains("std")))

## This step adds activity names to file
# first combine two files
master_activity_1 <- bind_rows(y_train, y_test)
# then join in code
master_activity_2 <- inner_join(master_activity_1, activity_labels, by = "V1" )
# drop unneeded columns
master_activity_2 <- select(master_activity_2, V2)
# append descriptions to mean_sd from master_activity_2 and add subject
subject_bind <- bind_rows(subject_train, subject_test)
final_detail1 <- bind_cols(master_activity_2, mean_sd)
final_detail2 <- bind_cols(subject_bind, final_detail1)
final_detail3 <- rename(final_detail2, subject = V1, activity_name = V2 )
```

Final step is summarizing data and exporting
```{r}
## Create final, tidy data set that groups by activity/subject and provides mean
tidy_data <- final_detail3 %>% group_by(activity_name, subject) %>% summarise_each(funs(mean))

write.table(tidy_data, "C:/Users/jbkessin/Documents/Get_Data_Proj/tidy_data.txt", sep="\t", row.name=FALSE)
```