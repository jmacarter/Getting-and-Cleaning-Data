Course Project Code Book
========================

Source of the data: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

Description of the data set: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

The attached R script (run_analysis.R) performs the following to clean up the data located in the downloaded and unzipped UCI HAR Dataset directory:

* Merges the training and the test sets to create one data set:
    * Merging train/X_train.txt with test/X_test.txt produces a 10299x561 data frame, as in the original description ("Number of Instances: 10299" and "Number of Attributes: 561"),
    * Merging train/subject_train.txt with test/subject_test.txt, results in a 10299x1 data frame with subject IDs,
    * Merging train/y_train.txt with test/y_test.txt yields a 10299x1 data frame with activity IDs.


* Extracts only the measurements on the mean and standard deviation for each measurement:
    * Read features.txt and extract only the measurements on the mean and standard deviation for each measurement.
    * The result is a 10299x66 data frame, as 66 out of 561 attributes are measurements on the mean and standard deviation. All measurements are floating point numbers in the range (-1, 1).


* Uses descriptive activity names to name the activities in the data set
    * Read activity_labels.txt and apply descriptive activity names to name the activities in the data set:

        walking
        
        walkingupstairs
        
        walkingdownstairs
        
        sitting
        
        standing
        
        laying


* Appropriately labels the data set with descriptive variable names.
    * Feature names (attributes) and activity names are converted to lower case, underscores and brackets () are removed
    * The code then merges the 10299x66 data frame containing features with 10299x1 data frames containing activity labels and subject IDs
    * The result is saved as merged_cleaned_data_with_names.txt, a 10299x68 data frame such that the first column contains subject IDs, the second column activity names, and the last 66 columns are measurements. Subject IDs are integers ranging between 1 and 30. The names of the attributes are similar to the following:

        tbodyacc-mean-x 
        
        tbodyacc-mean-y 
        
        tbodyacc-mean-z 
        
        tbodyacc-std-x 
        
        tbodyacc-std-y 
        
        tbodyacc-std-z 
        
        tgravityacc-mean-x 
        
        tgravityacc-mean-y


* From the merged and cleaned data set created above, creates a second, independent tidy data set with the average of each measurement for each activity and each subject.
    * The result is saved as tidy_data_set_with_the_averages.txt, a 180x68 data frame
    * The first column contains subject IDs, the second column contains activity names, and finally the averages for each of the 66 attributes are in columns 3 through 68. There are 30 subjects and 6 activities, thus 180 rows in this data set with averages.
