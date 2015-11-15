# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
step_data <- read.csv("activity.csv")
step_data <- subset(step_data, !is.na(steps))
```


## What is mean total number of steps taken per day?

```r
steps_per_day <- aggregate(step_data$steps, by=list(Date=step_data$date), FUN=sum)
names(steps_per_day) <- c("Date", "Steps")
hist(steps_per_day$Steps, xlab="Steps", main="Step Frequency")
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

The mean total number of steps taken per day is:

```r
mean(steps_per_day$Steps)
```

```
## [1] 10766.19
```

And the median total number of steps taken per day is:

```r
median(steps_per_day$Steps)
```

```
## [1] 10765
```

## What is the average daily activity pattern?

```r
average_steps <- aggregate(step_data$steps, by=list(Date=step_data$date), FUN=mean)
plot(average_steps, type="l", ylab="Average number of steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png) 

The highest average number of steps was on 2012-11-24.

## Imputing missing values

```r
step_data_with_na <- read.csv("activity.csv")
nas <- step_data_with_na[step_data_with_na$steps == "NA", ]
na_rows <- nrow(nas)
```
There are 2304 rows containing NA values.

## Are there differences in activity patterns between weekdays and weekends?
