# LSE_DA_NHS_analysis
## Week 2 Summary

Actual duration csv contained 137793 rows and 8 columns.
No NaN values were found in any of the columns.
As per metadata, duration less than 1 minute or greater than 60 mins 
are grouped as Unknown / Data Quality, this amount to 20161 rows, which is
15% of the appointments. This data if treated as outlier may give some insights of where duration is taken more.

Appointments Regional data did have any null values, it contained 596821 rows and 7 columns
From this dataset we found Unknown values in below columns
Unknown Appointment Status: 201324 => 33 % of records
Unknown HCP Type: 201324 => 33 % of records
Unknown Appointment Mode: 79147 => 13 % of records.

National Category data set has 817394 rows, 8 columns. No Unknown or null values found.

The below results were arrived, datasets were created from csv &  xls using
DataFrame read_csv & read+excel functions.
Null check is done using is nc[nc.isna().any(axis=1)]
metadata of the datasets are found using describe() & info()
counts were arrived using value_counts() and by filtering

Number of location : 106
High number of records (Top 5): 
       NHS North West London ICB - W2U3Z,
       NHS North East London ICB - A3A8R,
       NHS Kent and Medway ICB - 91Q,
       NHS Hampshire and Isle Of Wight ICB - D9Y0V,
       NHS South East London ICB - 72Q

Number of Service Settings:      5
Number of Context Types:         3
Number of National Categories:  18
Number of Appointment Status:     3 (Attended, Unknown, DNA )

## Week 3 Summary

Actual Duration & National Categories were analyzed.
appointment_date in actual_duration was converted to datetime format using pd.to_datetime()
Minimum and Maximum date in Actual Duration & Nation Categories were calulated by filtering by column and using min() & max().\

Minimum Date (Actual Duration) : 2021-12-01 00:00:00
Maximum Date (Actual Duration): 2022-06-30 00:00:00

Minimum Date (National Category): 2021-08-01 00:00:00
Maximum Date (National Category): 2022-06-30 00:00:00

Which service setting was the most popular for NHS North West London from 1 January to 1 June 2022?
eneral Practice              2104
Other                        1318
Primary Care Network         1272
Extended Access Provision    1090
Unmapped                      152
This is arrived by filtering by location name, appointment_date and grouping by sub_icb_location_name, service setting

Month with highest number of appointments: November

From the data analyzed it looks like more appointments are under service_setting 'General Practise'
The data also symbolizes the appointment count could be dependent on the season, with Winter & Autumn having more appointments.

## Week 4 Summary

National Categories were analyzed, visualizations were created using seaborn.
Line plots were created for  number of appointments per month for service settings, context types, and national categories.
This was done by grouping the data set by appointment_month & required.

The data insights from the graph shows the no of appointments increase by season, General Practise forms the major service used.
Care Relate Encounter forms major chunk of context type, General Consultation forms major national category.

Seasonal data are collected by grouping by required category & appointment_month and count_of_appointments were summed to get for specific category.
Its clear from the data that General Practise has more appointments than any category irrespective of the season.

## Week 5 Summary

Tweets related data were analyzed using dataframe methods, describe(), dtypes.
twitter full text was filtered from dataset, hashtags were found from the full text using string operations.
this data was converted to dataframe and no of occurrence of each  tags were found.
the hastag & count were put into a dataframe and bar chart was created to find which hashtag was trending.
Bar chart for least used hashtags were also plotted but these hastags were filtered so that its related to medicine.
From the twerets & hashtags we can find the health care & insurance forms the key hashtags used while tweeting.
People are more intrested to tweet abojut these tags, moreover the text on this tags can provide insights on what patients are looking for & which serivce setting.

## Week 6 Summary

Appointment_regional dataset was analyzed to find major concerns of NHS
appointment related columns were chosen and filtered from main dataset to understand the utilization data.
total no of appointments were calculated by grouping by appointment_month and aggregating using count
This dataset doesn't contain count_of_appointments hence sum() was not used.
utilization was calculated by average appointments per month.
Line plot was drawn, one could infer that begining of 2020 has more appointments, 
followed by inconsistent counts but lesser than begining of 2020.
Average Utilization also follows the trends similar to total count.
The total count is no where near the max NHS could handle as per this data set.
Other Practise Staff take more appointments, with GP following closely.

There is  Are there significant changes in whether or not visits are attended?
There is considerable no of appointment is in DNA or Unknown status. 
This needs to be looked into, there is a possibility if every GP follows common workflow the Unkown status may come down.

Are there changes in terms of appointment type and the busiest months?
Yes, end & begining of the year appointments are decreasing, otherewise increasing trend, except Unknown (this could be due to workflows followed by practise).
There has been reasonable increase in telephonic appointments.

Are there any trends in time between booking an appointment?
Yes there is a trend seen in the appointments. starts high in begining of the year, probably decreases begining of month but increases,
There seems to be a upward trend in more categories other than same day / one day appointment.

How do the spread of service settings compare?
Box plot was created for service_settings, appointment_mont & count.
The box plot was right skewed, with lots of outliers. When removed the outliers using showfliers=False option,
the plots looked better but still skewed towards right.  The mean looks positive in summer but more negative after the summer.
When removing the GP, out of service setting it looks much better & postive after removing outliers.
This provides insight that major issue is in General Practise, this is the place where the appointments go beyond a reasonable time causing more issues to NHS.