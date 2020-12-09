
Heart rate variability (HRV) is a measure of slight variations in heart rate - specifically, variation in inter-beat intervals. Having a high HRV is a sign of good overall health, whereas a low HRV is a sign of acute or chronic stress or fatigue. This project characterizes changes in HRV from a research study that tracked activities and heart rate data for volunteers engaged in normal daily activities. The aim of this project is to predict stressful vs restful activities based on HRV and actigraphy data, and to predict sleep disturbances using HRV and heart rate data.

# Pre-processing

Data for 22 volunteers were downloaded as .csv files from https://physionet.org/content/mmash/1.0.0/. Second-by-second activity data were labelled according to reported activities during specified time intervals throughout the day. Some heart rate outliers were removed if values were >= 2 standard deviations from the mean.

Data were parsed into time intervals of 1 minute or 5 minute durations, and mean actigraphy and heart rate scores were calculated for each interval. R-R intervals that inform about heart rate variability were parsed into these 1 or 5 minute intervals to determine how heart rate variability changes from one time interval to the next. The R-R data were filtered to remove very high or very low values and filtered a second time to remove values outside one standard deviation from the mean within each interval. A HRV summary metric root mean square of successive differences (RMSSD) was calculated for each time interval.

# Model

To predict stressful and restful periods during the day, 5 minute intervals were labelled based on the user's activity. Exercise, alcohol use, and smoking were labelled as stressful activities, and laying down and sitting were labelled as restful activities. Features to predict stress vs rest were mean HRV and mean actigraphy score for each interval.

To predict sleep disturbances, 10 minute rolling time periods were identified in which six one-minute periods were sampled. Each 10 minute period was labelled as having a sleep disturbance if actigraphy data indicate movement in the last minute of the time interval. Intervals were labelled as not having a sleep disturbance if actigraphy data indicate no movement during any of the sampled times.

# Results

Two Random Forest Classification models were created, one to predict stress vs rest during the day, and one to predict sleep disturbances at night. The model to predict stress vs rest had an overall accuracy of 0.86, precision of 0.84, and recall of 0.87. These data show that overall, we can predict stressful events fairly accurately using movement and HRV data.

The model to predict sleep disturbances using only HRV and HR data also performs well with an overall accuracy of 0.89, precision of 0.87, and recall of 0.91. Because HRV is quite variable over time, there are some false positives where HRV suggests a sleep disturbance even when there is none. Nonetheless, using a fairly small feature set, we can identify individual sleep disturbances quite well.

# References

Rossi, A., Da Pozzo, E., Menicagli, D., Tremolanti, C., Priami, C., Sirbu, A., Clifton, D., Martini, C., & Morelli, D. (2020). Multilevel Monitoring of Activity and Sleep in Healthy People (version 1.0.0). PhysioNet. https://doi.org/10.13026/cerq-fc86.
