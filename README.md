# Overview

This is my final project for the Data Input and Manipulation course at Georgia
Tech. The main purpose of this course is to web scrape data sets online (I used
Selnium and BeautifulSoup) and use
Python libraries such as numpy and pandas to clean and analysis the data. I
also used the plotly library to create visualizations for my cleaned data. 

![onePager](https://github.com/spausum/consumer-spending-analysis/assets/121176362/e1c8f85c-8093-4005-976f-007042a41a12)

# Research Question

How did the COVID pandemic impact consumer spending in the United States. Are
these changes in consumer behavior, if any, consistent among different
countries? Were the changes in spending different based on spending categories
such as essential versus non-essential goods.

# Data Collection

I webscraped three websites and collected a csv file. The cvs file, which I
collected from the US government travel site, contained flight information such
as departuture and arrival cities, number of passengers, and cost per flight for
different years dating back to 1993.

The first website I webscaped was the [JSON API](https://stats.oecd.org/SDMX-JSON/data/SNA_TABLE5/AUS+AUT+BEL+CAN+CHL+COL+CRI+CZE+DNK+EST+FIN+FRA+DEU+GRC+HUN+ISL+IRL+ISR+ITA+JPN+KOR+LVA+LTU+LUX+MEX+NLD+NZL+NOR+POL+PRT+SVK+SVN+ESP+SWE+CHE+TUR+GBR+USA+EU27_2020+NMEC+BRA+CHN+IND+IDN+RUS+SAU+ZAF.P31NC+P31DC+P31CP010+P31CP011+P31CP012+P31CP020+P31CP021+P31CP022+P31CP023+P31CP030+P31CP031+P31CP032+P31CP040+P31CP041+P31CP042+P31CP043+P31CP044+P31CP045+P31CP050+P31CP051+P31CP052+P31CP053+P31CP054+P31CP055+P31CP056+P31CP060+P31CP061+P31CP062+P31CP063+P31CP070+P31CP071+P31CP072+P31CP073+P31CP080+P31CP081+P31CP082+P31CP083+P31CP090+P31CP091+P31CP092+P31CP093+P31CP094+P31CP095+P31CP096+P31CP100+P31CP101+P31CP102+P31CP103+P31CP104+P31CP105+P31CP110+P31CP111+P31CP112+P31CP120+P31CP121+P31CP122+P31CP123+P31CP124+P31CP125+P31CP126+P31CP127+P31CP122_127+P311+P312+P313+P311B+P312B+P313B+P314B+P33+P34+B1_GE.C+V+VP+VOB/all?startTime=2008&endTime=2022&dimensionAtObservation=allDimensions&pid=23412a5b-ef0e-4d5e-a011-dfa9066ebd40) from the 
[OECD](https://stats.oecd.org/Index.aspx?DataSetCode=SNA_TABLE5#). This provided
final expenditure of households each year for different countries.

My second website was this table from the [National Center for Biotechnology
Information](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9381923/table/T1/?report=objectonly).
This table gave break down of food spending categories based on different
demographics.

My final website was country codes from
[IBAN](https://www.iban.com/country-codes). It mainly served to assist in my
Geographical visualization of my data.

# Data Cleaning

Within my datasets, there were a couple of inconsistencies.

1. Within my downloaded CSV file, there were two columns: "Geocoded_City1" and 
"Geocoded_City2" which had NaN values in certain rows while other rows of the 
same cities had valid values. To fix this inconsistency, I created a dictionary 
(geo_dict) with each "citymarketid" as a key and its values as its Geolocation. 
Then for each row within my DataFrame if the "citymarketid" was in my dictionary, 
I replaced "Geocoded_City1" and "Geocoded_City2" with the value corresponding 
to the citymarketid to replace NaN values using the apply method and a lambda expresson.

2. Within my downloaded CSV file, my "Geocoded_City1" and "Geocoded_City2" had 
the city name seperated by "\n" with its coordinates. These coorinates would be 
useful for data visualization so I decided to seperate these columns into two 
three seperate columns: one for the city name, one for latitude, and one for 
longitude. I used the .str.split("", expand = True) to seperate the columns 
and casted the coordinates as floats while keeping the city name as a string.

3. My first web collection site contained a JSON dictionary where the values 
was a list with mixed in with with floats, 0s and nulls. I checked for 
non-zero floats within the lists and only used those for my pandas DataFrame.

# Data Visualizations

![european_expense](https://github.com/spausum/consumer-spending-analysis/assets/121176362/a8d4d075-fdad-4c94-8d78-b1d7b9fcda59)
![2019_flight_paths](https://github.com/spausum/consumer-spending-analysis/assets/121176362/2096c1a4-9ceb-4cb6-8634-491e5dd96774)
![2020_flight_paths](https://github.com/spausum/consumer-spending-analysis/assets/121176362/edfc0c7c-9b8f-4650-97c8-f5d3ca4e48b2)
![flight_revenue](https://github.com/spausum/consumer-spending-analysis/assets/121176362/00414255-4083-49bf-883e-952f81c2cb5e)
![food_spending](https://github.com/spausum/consumer-spending-analysis/assets/121176362/36e18166-3b34-4008-bb94-37f43d25227a)


