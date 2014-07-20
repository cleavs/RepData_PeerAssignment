Reproducible Research Peer Assignment 1
========================================================
Loading and preprocessing the data



```r
fileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
download.file(fileUrl, destfile = "activity.zip", method = "curl")
unzip("activity.zip")
activity <- read.csv("activity.csv")
```


Here is the mean total number of steps taken per day?


```
## [1] 10766
```


Here is a histogram of the total number of steps taken each day
![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

Mean and Median total number of steps taken per day



```
## [1] 10766
```

```
## [1] 10765
```


Here is the average daily activity pattern?
![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 

Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
maxInterval <- avgInterval[which.max(avgInterval$steps), ]$interval
maxInterval
```

```
## [1] 835
```

Imputing missing values:
Total missing values

```r
missing <- sum(is.na(activity))
missing
```

```
## [1] 2304
```

Filling the missing values

```r
newActivity = activity
newActivity[is.na(newActivity)] <- mean(totalSteps$steps)
summary(newActivity)
```

```
##      steps               date          interval   
##  Min.   :    0   2012-10-01:  288   Min.   :   0  
##  1st Qu.:    0   2012-10-02:  288   1st Qu.: 589  
##  Median :    0   2012-10-03:  288   Median :1178  
##  Mean   : 1444   2012-10-04:  288   Mean   :1178  
##  3rd Qu.:   57   2012-10-05:  288   3rd Qu.:1766  
##  Max.   :10766   2012-10-06:  288   Max.   :2355  
##                  (Other)   :15840
```


Create histogram and new mean and median

```r
newSteps <- aggregate(steps ~ date, data = newActivity, sum)
hist(newSteps$steps, main = "New steps per day", xlab = "Steps per day", col = "blue")
```

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9.png) 

```r
mean(newSteps$steps)
```

```
## [1] 415998
```

```r
median(newSteps$steps)
```

```
## [1] 11458
```

Are there any difference in Activity patterns ? 


