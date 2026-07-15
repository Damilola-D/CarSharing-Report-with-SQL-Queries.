# CarSharing-Report-with-SQL-Queries.      

Google Drive Folder Link:
https://drive.google.com/drive/folders/1ENSq4EiioNS1Z2oVHYJqnplNF_e0nbD7?usp=sharing

Question
Create relationships between the tables by linking the temperature, weather and time tables to the CarSharing_df table.
SQL Query:
SELECT * FROM CarSharing_df c JOIN Time t ON c.id =t.id JOIN weather w ON c.weather_code = w.weather_code JOIN Temperature temp ON c.temp_code = temp.temp_code

Question (a): Please tell me which date and time we had the highest demand rate in 2017.
SQL Query: 
SELECT t.timestamp, c.demand FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' ORDER BY c.demand DESC LIMIT 1;
Result:
https://drive.google.com/file/d/1_dcw7_SrilgIeFULNaKtmb8haRPiOs8J/view?usp=drive_link
Interpretation: we had the highest demand rate in 2017-06-15 17:00:00 

Question (b): Give me a table containing the name of the weekday, month, and season in which we had the highest and lowest average demand throughout 2017. Please include the calculated average demand values as well.
SQL Query:
SELECT t. "weekday name" AS Weekday, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY t."weekday name" ORDER BY Average_Demand DESC;
Result:
https://drive.google.com/file/d/1sG2Z8n0rdG14YdNzn0P64lAYy0Xq3xz9/view?usp=drive_link
SQL Query:
SELECT t. "month name" AS Month, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY t."month name" ORDER BY Average_Demand DESC;
Result:
https://drive.google.com/file/d/1nZ6rctL4DRDVkTwzpWE93mb5xr5CT27x/view?usp=drive_link
SQL Query:
SELECT t.season, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY t.season ORDER BY Average_Demand DESC;
Result:
https://drive.google.com/file/d/1M15u_Yrvw2HJICz_OLfkVdDTzkultBWp/view?usp=drive_link

Question (c) 
For the weekday(s) selected in (b), please give me a table showing the average demand we had at different hours of that weekday throughout 2017. Please sort the results in descending order based on the average demand.
SQL Query:
SElECT t.hour, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' AND t."weekday name" = 'Sunday' GROUP BY t.hour ORDER BY Average_Demand DESC;
Result:
https://drive.google.com/file/d/1D2NrlwAXcFeSznVaKh0TR2mYwJwBMIS3/view?usp=drive_link
SQL Query
SElECT t.hour, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' AND t."weekday name" = 'Thursday' GROUP BY t.hour ORDER BY Average_Demand DESC;
Result:
https://drive.google.com/file/d/1D2NrlwAXcFeSznVaKh0TR2mYwJwBMIS3/view?usp=drive_link
Interpretation:
The weekday with the highest average demand in 2017 was Sunday, while the weekday with the lowest average demand was Thursday. The tables show the average demand for each hour of the day on these weekdays, sorted in descending order of average demand.

Question (d) 
Please tell me what the weather was like in 2017. Was it mostly cold, mild, or hot? which weather condition (shown in the weather column) was the most prevalent in 2017? What was the average, highest, and lowest wind speed and humidity for each month in 2017? Please organize this information in two tables for the wind speed and humidity. Please also give me a table showing the average demand for each cold, mild, and hot weather in 2017 sorted in descending order based on their average demand.
Please tell me what the weather was like in 2017. Was it mostly cold, mild, or hot?
SQL Query:
SELECT temp.temp_category, COUNT(*) AS Frequency FROM CarSharing_df c JOIN Time t ON c.id = t.id JOIN Temperature temp ON c.temp_code = temp.temp_code WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY temp.temp_category ORDER BY Frequency DESC;
Result:
https://drive.google.com/file/d/1LFFNbG4Som5-eBV28sELGMlnSDi8VFUO/view?usp=drive_link
Interpretation:
The most prevalent temperature category in 2017 was Hot.

which weather condition (shown in the weather column) was the most prevalent in 2017? 
SQL Query:
SELECT w.weather, COUNT(*) AS Frequency FROM CarSharing_df c JOIN Time t ON c.id = t.id JOIN Weather w ON c. weather_code = w.weather_code WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY w.weather ORDER BY Frequency DESC;
Result:
https://drive.google.com/file/d/1HEOUOu-QmV_whfEvjpjgn8d4nqJGvKLD/view?usp=drive_link
Interpretation:
The most prevalent weather condition in 2017 was Clear or partly cloudy, occurring 2,114 times.

What was the average, highest, and lowest wind speed for each month in 2017?
SQL Query:
SELECT t. "month name" AS Month, ROUND(AVG(c.windspeed), 2) AS Average_WindSpeed, ROUND(MAX(c.windspeed), 2) AS Highest_WindSpeed, ROUND(MIN(c.windspeed), 2) AS Lowest_WindSpeed FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY t."month name" ORDER BY MIN(t.timestamp);
Result:
https://drive.google.com/file/d/1IS1s-6t8jQVgh644heEDaBLpJbnG6S17/view?usp=drive_link

What was the average, highest, and lowest humidity for each month in 2017?
SQL Query:
SELECT t. "month name" AS Month, ROUND(AVG(c.humidity), 2) AS Average_Humidity, ROUND(MAX(c.humidity), 2) AS Highest_Humidity, ROUND(MIN(c.humidity), 2) AS Lowest_Humidity FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY t."month name" ORDER BY MIN(t.timestamp);
Result:
https://drive.google.com/file/d/1YVpyNHWPtGuGyfTUg2a00VGKa0xmfQkE/view?usp=drive_link

Please also give me a table showing the average demand for each cold, mild, and hot weather in 2017 sorted in descending order based on their average demand.
SQL Query:
SELECT temp.temp_category AS Temperature, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id JOIN Temperature temp ON c.temp_code = temp.temp_code WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY temp.temp_category ORDER BY Average_Demand DESC;
Result
https://drive.google.com/file/d/1yE_fOV2YBHG2iaIwUdH98nXK7wJWoJ1O/view?usp=drive_link
Interpretation:
The analysis shows that Hot temperatue conditions recorded the highest average car-sharing demand (5.36), followed by Mild conditions (4.70). Cold temperatures had the lowest average demand (3.90). 


Question (e).
Give me another table showing the information requested in (d) for the month we had the highest average demand in 2017 so that I can compare it with other months.
SQL Query:
SELECT t."month name" AS Month, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id WHERE strftime('%Y', t.timestamp) = '2017' GROUP BY t."month name" ORDER BY Average_Demand DESC;
Result:
https://drive.google.com/file/d/1IWTPfhvQ_ZHX_Upyd0E5y43GlGl9oNAN/view?usp=drive_link
Result:
July has the highest average demand in 2017

Average demand for each temperature category in July
SQL Query:
SELECT temp.temp_category AS Temperature, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id JOIN Temperature temp ON c.temp_code = temp.temp_code WHERE strftime('%Y', t.timestamp) = '2017' AND t."month name" = 'July' GROUP BY temp.temp_category ORDER BY Average_Demand DESC; 
Result:
https://drive.google.com/file/d/148OZzIg27XHbWiFLPZa3fsnnANQc308g/view?usp=drive_link
Interpretation:
For July, which had the highest average demand in 2017, the Mild temperature category recorded the highest average demand (5.62), followed closely by the Hot category (5.50). There were no Cold temperatue observations during July. Compared with the overall 2017 analysis, where Hot temperaures had the highest average demand was slighly higher under Mild temperatures, indicating that comfortable weather conditions may have encouraged greater usea of car-sharing service during the month with the highest demand. 






SQL Query
SELECT temp.temp_category AS Temperature, ROUND(AVG(c.demand), 2) AS Average_Demand FROM CarSharing_df c JOIN Time t ON c.id = t.id JOIN Temperature temp ON 
