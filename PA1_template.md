---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---
## Loading and preprocessing the data
First, the file is unziped and saved into a dataframe variable. 

```r
unzip('activity.zip')
activity <- read.csv('activity.csv')
```

It will be necessary to have a NA clean dataframe of the data:

```r
activity_clean <- na.omit(activity)
head(activity_clean)
```

```
##     steps       date interval
## 289     0 2012-10-02        0
## 290     0 2012-10-02        5
## 291     0 2012-10-02       10
## 292     0 2012-10-02       15
## 293     0 2012-10-02       20
## 294     0 2012-10-02       25
```

## What is mean total number of steps taken per day?
Before showing the mean total number of steps per day, the sum of steps per day is showed:
First, a dataframe with the number of steps per day is created.

```r
steps_day <- aggregate(activity_clean$steps, list(activity_clean$date), sum)
library(stringr)
steps_day$Group.1 <- as.numeric(str_sub(steps_day$Group.1, start= -2))
head(steps_day)
```

```
##   Group.1     x
## 1       2   126
## 2       3 11352
## 3       4 12116
## 4       5 13294
## 5       6 15420
## 6       7 11015
```

The histogram showing the number of steps per day (lacking values because of NAs):

```r
barplot(height=steps_day$x, names=steps_day$Group.1,
        main='Total number of steps', xlab='Days 10/2012', ylab='Steps') 
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

The mean and median of the steps per day:

```r
mean(steps_day$x)
```

```
## [1] 10766.19
```

```r
median(steps_day$x)
```

```
## [1] 10765
```

## What is the average daily activity pattern?

Now it is going to be showed the average of steps per interval of time across all the days. To do that, it is necessary to make 
a dataframe with the mean of steps per interval first:

```r
steps_interval <- aggregate(activity_clean$steps, list(activity_clean$interval), mean)

library(dygraphs)
dygraph(steps_interval, main='Average number of steps per interval',
        xlab='Time intervals', ylab='Average of steps')
```

```{=html}
<div class="dygraphs html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-6160ff407d633895b99c" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-6160ff407d633895b99c">{"x":{"attrs":{"title":"Average number of steps per interval","xlabel":"Time intervals","ylabel":"Average of steps","labels":["Group.1","x"],"legend":"auto","retainDateWindow":false,"axes":{"x":{"pixelsPerLabel":60}}},"annotations":[],"shadings":[],"events":[],"format":"numeric","data":[[0,5,10,15,20,25,30,35,40,45,50,55,100,105,110,115,120,125,130,135,140,145,150,155,200,205,210,215,220,225,230,235,240,245,250,255,300,305,310,315,320,325,330,335,340,345,350,355,400,405,410,415,420,425,430,435,440,445,450,455,500,505,510,515,520,525,530,535,540,545,550,555,600,605,610,615,620,625,630,635,640,645,650,655,700,705,710,715,720,725,730,735,740,745,750,755,800,805,810,815,820,825,830,835,840,845,850,855,900,905,910,915,920,925,930,935,940,945,950,955,1000,1005,1010,1015,1020,1025,1030,1035,1040,1045,1050,1055,1100,1105,1110,1115,1120,1125,1130,1135,1140,1145,1150,1155,1200,1205,1210,1215,1220,1225,1230,1235,1240,1245,1250,1255,1300,1305,1310,1315,1320,1325,1330,1335,1340,1345,1350,1355,1400,1405,1410,1415,1420,1425,1430,1435,1440,1445,1450,1455,1500,1505,1510,1515,1520,1525,1530,1535,1540,1545,1550,1555,1600,1605,1610,1615,1620,1625,1630,1635,1640,1645,1650,1655,1700,1705,1710,1715,1720,1725,1730,1735,1740,1745,1750,1755,1800,1805,1810,1815,1820,1825,1830,1835,1840,1845,1850,1855,1900,1905,1910,1915,1920,1925,1930,1935,1940,1945,1950,1955,2000,2005,2010,2015,2020,2025,2030,2035,2040,2045,2050,2055,2100,2105,2110,2115,2120,2125,2130,2135,2140,2145,2150,2155,2200,2205,2210,2215,2220,2225,2230,2235,2240,2245,2250,2255,2300,2305,2310,2315,2320,2325,2330,2335,2340,2345,2350,2355],[1.716981132075472,0.3396226415094339,0.1320754716981132,0.1509433962264151,0.07547169811320754,2.09433962264151,0.5283018867924528,0.8679245283018868,0,1.471698113207547,0.3018867924528302,0.1320754716981132,0.3207547169811321,0.6792452830188679,0.1509433962264151,0.3396226415094339,0,1.113207547169811,1.830188679245283,0.169811320754717,0.169811320754717,0.3773584905660378,0.2641509433962264,0,0,0,1.132075471698113,0,0,0.1320754716981132,0,0.2264150943396226,0,0,1.547169811320755,0.9433962264150944,0,0,0,0,0.2075471698113208,0.6226415094339622,1.622641509433962,0.5849056603773585,0.4905660377358491,0.07547169811320754,0,0,1.188679245283019,0.9433962264150944,2.566037735849056,0,0.3396226415094339,0.3584905660377358,4.113207547169812,0.660377358490566,3.490566037735849,0.8301886792452831,3.113207547169811,1.113207547169811,0,1.566037735849057,3,2.245283018867925,3.320754716981132,2.962264150943396,2.09433962264151,6.056603773584905,16.0188679245283,18.33962264150943,39.45283018867924,44.49056603773585,31.49056603773585,49.26415094339622,53.77358490566038,63.45283018867924,49.9622641509434,47.0754716981132,52.15094339622642,39.33962264150944,44.0188679245283,44.16981132075472,37.35849056603774,49.0377358490566,43.81132075471698,44.37735849056604,50.50943396226415,54.50943396226415,49.9245283018868,50.9811320754717,55.67924528301887,44.32075471698113,52.26415094339622,69.54716981132076,57.84905660377358,56.15094339622642,73.37735849056604,68.20754716981132,129.4339622641509,157.5283018867925,171.1509433962264,155.3962264150943,177.3018867924528,206.1698113207547,195.9245283018868,179.5660377358491,183.3962264150943,167.0188679245283,143.4528301886793,124.0377358490566,109.1132075471698,108.1132075471698,103.7169811320755,95.9622641509434,66.20754716981132,45.22641509433962,24.79245283018868,38.75471698113208,34.9811320754717,21.05660377358491,40.56603773584906,26.9811320754717,42.41509433962264,52.66037735849056,38.9245283018868,50.79245283018868,44.28301886792453,37.41509433962264,34.69811320754717,28.33962264150943,25.09433962264151,31.94339622641509,31.35849056603774,29.67924528301887,21.32075471698113,25.54716981132075,28.37735849056604,26.47169811320755,33.43396226415094,49.9811320754717,42.0377358490566,44.60377358490566,46.0377358490566,59.18867924528302,63.86792452830188,87.69811320754717,94.84905660377359,92.77358490566037,63.39622641509434,50.16981132075472,54.47169811320754,32.41509433962264,26.52830188679245,37.73584905660378,45.0566037735849,67.28301886792453,42.33962264150944,39.88679245283019,43.26415094339622,40.9811320754717,46.24528301886792,56.43396226415094,42.75471698113208,25.13207547169811,39.9622641509434,53.54716981132076,47.32075471698113,60.81132075471698,55.75471698113208,51.9622641509434,43.58490566037736,48.69811320754717,35.47169811320754,37.54716981132076,41.84905660377358,27.50943396226415,17.11320754716981,26.07547169811321,43.62264150943396,43.77358490566038,30.0188679245283,36.0754716981132,35.49056603773585,38.84905660377358,45.9622641509434,47.75471698113208,48.13207547169812,65.32075471698113,82.90566037735849,98.66037735849056,102.1132075471698,83.9622641509434,62.13207547169812,64.13207547169812,74.54716981132076,63.16981132075472,56.90566037735849,59.77358490566038,43.86792452830188,38.56603773584906,44.66037735849056,45.45283018867924,46.20754716981132,43.67924528301887,46.62264150943396,56.30188679245283,50.71698113207547,61.22641509433962,72.71698113207547,78.94339622641509,68.94339622641509,59.66037735849056,75.09433962264151,56.50943396226415,34.77358490566038,37.45283018867924,40.67924528301887,58.0188679245283,74.69811320754717,85.32075471698113,59.26415094339622,67.77358490566037,77.69811320754717,74.24528301886792,85.33962264150944,99.45283018867924,86.58490566037736,85.60377358490567,84.86792452830188,77.83018867924528,58.0377358490566,53.35849056603774,36.32075471698113,20.71698113207547,27.39622641509434,40.0188679245283,30.20754716981132,25.54716981132075,45.66037735849056,33.52830188679246,19.62264150943396,19.0188679245283,19.33962264150943,33.33962264150944,26.81132075471698,21.16981132075472,27.30188679245283,21.33962264150943,19.54716981132075,21.32075471698113,32.30188679245283,20.15094339622642,15.94339622641509,17.22641509433962,23.45283018867925,19.24528301886792,12.45283018867925,8.018867924528301,14.66037735849057,16.30188679245283,8.679245283018869,7.79245283018868,8.132075471698114,2.622641509433962,1.452830188679245,3.679245283018868,4.811320754716981,8.509433962264151,7.075471698113208,8.69811320754717,9.754716981132075,2.207547169811321,0.3207547169811321,0.1132075471698113,1.60377358490566,4.60377358490566,3.30188679245283,2.849056603773585,0,0.8301886792452831,0.9622641509433962,1.584905660377359,2.60377358490566,4.69811320754717,3.30188679245283,0.6415094339622641,0.2264150943396226,1.075471698113208]]},"evals":[],"jsHooks":[]}</script>
```

It is interesting to know the time interval that contains, on average, the maximum number of steps:

```r
steps_interval[steps_interval$x==max(steps_interval$x),]
```

```
##     Group.1        x
## 104     835 206.1698
```

## Imputing missing values
There is only one column in the dataframe with NAs:

```r
sum(is.na(activity))
```

```
## [1] 2304
```

```r
sum(is.na(activity$steps))
```

```
## [1] 2304
```

The chosen strategy to fill the NAs values is to introduce in each empty time interval the mean of in that interval for the 
rest of days.

```r
steps_interval <- aggregate(activity_clean$steps, list(activity_clean$interval), mean)
head(steps_interval)
```

```
##   Group.1         x
## 1       0 1.7169811
## 2       5 0.3396226
## 3      10 0.1320755
## 4      15 0.1509434
## 5      20 0.0754717
## 6      25 2.0943396
```

```r
activity_filled <- activity
activity_filled$steps <- ifelse(is.na(activity_filled$steps),
                         steps_interval$x[match(activity$interval, steps_interval$Group.1)],
                         activity_filled$steps)
```

To make the histogram it is necessary to create a dataframe wit the sum of steps per day with the updated dataframe.

```r
steps_day_filled <- aggregate(activity_filled$steps, list(activity_filled$date), sum)
steps_day_filled$Group.1 <- as.numeric(str_sub(steps_day_filled$Group.1, start= -2))
head(steps_day_filled)
```

```
##   Group.1        x
## 1       1 10766.19
## 2       2   126.00
## 3       3 11352.00
## 4       4 12116.00
## 5       5 13294.00
## 6       6 15420.00
```

Finally, the histogram and mean and median values can be obtained. 

```r
barplot(height=steps_day_filled$x, names=steps_day_filled$Group.1,
        main='Total number of steps per day filling NAs', xlab='Days 10/2012', ylab='Steps') 
```

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

```r
mean(steps_day_filled$x)
```

```
## [1] 10766.19
```

```r
median(steps_day_filled$x)
```

```
## [1] 10766.19
```


## Are there differences in activity patterns between weekdays and weekends?

It is necessary to create a dataframe with the intervals and number of steps having a column that specifies if it is weekday or weekend.

```r
activity_filled$weekday <- weekdays(as.POSIXct(activity_filled$date))
head(activity_filled)
```

```
##       steps       date interval weekday
## 1 1.7169811 2012-10-01        0  Monday
## 2 0.3396226 2012-10-01        5  Monday
## 3 0.1320755 2012-10-01       10  Monday
## 4 0.1509434 2012-10-01       15  Monday
## 5 0.0754717 2012-10-01       20  Monday
## 6 2.0943396 2012-10-01       25  Monday
```

```r
days_w <- unique(activity_filled$weekday)
weekday <- c(days_w[1:5])
weekend <- c(days_w[6:7])

steps_weekend <- activity_filled[activity_filled$weekday %in% weekend,]
steps_interval_weekend <- aggregate(steps_weekend$steps, list(steps_weekend$interval), sum)
head(steps_interval_weekend)
```

```
##   Group.1          x
## 1       0  3.4339623
## 2       5  0.6792453
## 3      10  0.2641509
## 4      15  0.3018868
## 5      20  0.1509434
## 6      25 56.1886792
```

```r
steps_weekday <- activity_filled[activity_filled$weekday %in% weekday,]
steps_interval_weekday <- aggregate(steps_weekday$steps, list(steps_weekday$interval), sum)
head(steps_interval_weekday)
```

```
##   Group.1          x
## 1       0 101.301887
## 2       5  20.037736
## 3      10   7.792453
## 4      15   8.905660
## 5      20   4.452830
## 6      25  71.566038
```

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
steps_interval_weekday$part_week <- 'Weekday'
steps_interval_weekend$part_week <- 'Weekend'
steps_interval_wdwk <- bind_rows(steps_interval_weekday, steps_interval_weekend)
head(steps_interval_wdwk)
```

```
##   Group.1          x part_week
## 1       0 101.301887   Weekday
## 2       5  20.037736   Weekday
## 3      10   7.792453   Weekday
## 4      15   8.905660   Weekday
## 5      20   4.452830   Weekday
## 6      25  71.566038   Weekday
```


The time series plot can be created:

```r
library(ggplot2)
ggplot(steps_interval_wdwk, aes(x = Group.1, y = x)) +
  geom_line(position='identity') +
  facet_grid(. ~ part_week)+
  labs(title='Number of steps per interval (NAs filled)', x='Interval', y='Steps')+
  theme(plot.title = element_text(hjust = 0.5))
```

![](PA1_template_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


















