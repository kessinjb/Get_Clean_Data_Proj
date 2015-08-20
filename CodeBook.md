---
title: "CodeBook"
author: "john_kessing"
date: "Wednesday, August 19, 2015"
output: html_document
---

This CodeBook.md lists basic information related to the creation of the tidy_data dataset.  For detailed information on the scripts, please refer to the ReadMe.md.

## Creation of tidy_data set:
The following are key steps taken to create the tidy_data dataset:
- Loaded all information and combined separate files to create a single data set
  - Subject information and activity descriptions existed in other files
- Added descriptive column headers and cleaned up column header names
  - Column header names included punctuation and other undesirable characters which were removed
  - Column headers contained abreviations, which were expanded to include full information
    - Acc changed to acclerometer
    - Gyro changed to gyroscope
    - Mag changed to magnitude
    - BodyBody changed to body
- Selected only columns to means and standard deviations
  - Leveraged a function to only select columns containing these
  - Also included calculated columns leveraged to calculate mean (e.g. ..JerkMean and FreqMean)
- Summarized data by activity type and subject
  - Other columns are averages of all recorded data

## tidy_data data elements:
# First two are descriptors
activity_name - activity people were performing while wearing phone
subject - identifier representing which volunteer was performing test
# following columns represent measurement data, columns beginning with t represent time while columns starting with g represent acceleration
tBodyaccelerometermeanX
tBodyaccelerometermeanY
tBodyaccelerometermeanZ
tGravityaccelerometermeanX
tGravityaccelerometermeanY
tGravityaccelerometermeanZ
tBodyaccelerometerJerkmeanX
tBodyaccelerometerJerkmeanY
tBodyaccelerometerJerkmeanZ
tBodygyroscopemeanX
tBodygyroscopemeanY
tBodygyroscopemeanZ
tBodygyroscopeJerkmeanX
tBodygyroscopeJerkmeanY
tBodygyroscopeJerkmeanZ
tBodyaccelerometermagnitudemean
tGravityaccelerometermagnitudemean
tBodyaccelerometerJerkmagnitudemean
tBodygyroscopemagnitudemean
tBodygyroscopeJerkmagnitudemean
fBodyaccelerometermeanX
fBodyaccelerometermeanY
fBodyaccelerometermeanZ
fBodyaccelerometermeanFreqX
fBodyaccelerometermeanFreqY
fBodyaccelerometermeanFreqZ
fBodyaccelerometerJerkmeanX
fBodyaccelerometerJerkmeanY
fBodyaccelerometerJerkmeanZ
fBodyaccelerometerJerkmeanFreqX
fBodyaccelerometerJerkmeanFreqY
fBodyaccelerometerJerkmeanFreqZ
fBodygyroscopemeanX
fBodygyroscopemeanY
fBodygyroscopemeanZ
fBodygyroscopemeanFreqX
fBodygyroscopemeanFreqY
fBodygyroscopemeanFreqZ
fBodyaccelerometermagnitudemean
fBodyaccelerometermagnitudemeanFreq
fbodyaccelerometerJerkmagnitudemean
fbodyaccelerometerJerkmagnitudemeanFreq
fbodygyroscopemagnitudemean
fbodygyroscopemagnitudemeanFreq
fbodygyroscopeJerkmagnitudemean
fbodygyroscopeJerkmagnitudemeanFreq
angletBodyaccelerometerMeangravity
angletBodyaccelerometerJerkMeangravityMean
angletBodygyroscopeMeangravityMean
angletBodygyroscopeJerkMeangravityMean
angleXgravityMean
angleYgravityMean
angleZgravityMean
tBodyaccelerometerstdX
tBodyaccelerometerstdY
tBodyaccelerometerstdZ
tGravityaccelerometerstdX
tGravityaccelerometerstdY
tGravityaccelerometerstdZ
tBodyaccelerometerJerkstdX
tBodyaccelerometerJerkstdY
tBodyaccelerometerJerkstdZ
tBodygyroscopestdX
tBodygyroscopestdY
tBodygyroscopestdZ
tBodygyroscopeJerkstdX
tBodygyroscopeJerkstdY
tBodygyroscopeJerkstdZ
tBodyaccelerometermagnitudestd
tGravityaccelerometermagnitudestd
tBodyaccelerometerJerkmagnitudestd
tBodygyroscopemagnitudestd
tBodygyroscopeJerkmagnitudestd
fBodyaccelerometerstdX
fBodyaccelerometerstdY
fBodyaccelerometerstdZ
fBodyaccelerometerJerkstdX
fBodyaccelerometerJerkstdY
fBodyaccelerometerJerkstdZ
fBodygyroscopestdX
fBodygyroscopestdY
fBodygyroscopestdZ
fBodyaccelerometermagnitudestd
fbodyaccelerometerJerkmagnitudestd
fbodygyroscopemagnitudestd
fbodygyroscopeJerkmagnitudestd
