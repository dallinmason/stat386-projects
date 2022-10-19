---
layout: post
title:  "A Walkthrough of Obtaining Past Weather Data for Salt Lake City"
date:   2022-10-18
author: Dallin Mason
description: A great explanation about how to scrape a website in order to obtain past weather data.
image: /assets/images/Storm.jpeg
---

# A Walkthrough of Obtaining Past Weather Data for Salt Lake City

<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Fall.jpg" alt="" style="width:500px;"/>

Weather plays an important factor in decision making whether we consciously choose to ignore it 
or not. Thus an analysis of the past weather can be valuable. This is of great interest to many people 
as it can help predict how certain holidays such as Halloween or Thanksgiving might play out. Will it 
be too warm or too cold to eat outside? Does there appear to be much wind during these transition months?
All of these questions and more we hope to be able to explain with this dataset which we will gather and use here in future posts.


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/License.jpg" alt="" style="width:250px;"/>

First off it is important to understand a little bit about the climate of Utah. Utah is a state that always claims to have the greatest snow on Earth. It proudly bears all 4 seasons and the almost the majority of the year is spent during the winter months due to its being part of the Rocky Mountain region of the United States. Summers generally don't rise about 102 °F during their hottest parts and winter temperatures generally never dip below 0 °F. Precipitation is most common in the form of snow which can be quite frequent during the winter months which is always very well celebrated by avid skiers and snow-boarders. An occasional thunderstorm can provide relief during the scorching months of summer though. 


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Ski.jpg" alt="" style="width:500px;"/>


Overall, the weather does very quite a bit from one part of the year to another which is a motivation for our question of interest. We would like to analyze past weather data from the transition from summer into fall to determine any major differences between temperatures, barometric pressure, windspeed, humidity, and dew point and to see if these factors can help us explain how this beautiful transition occurs.  


## Objective
So in deciding how to go about obtaining the past weather in Salt Lake City we went to several websites
to be able to decide which one worked best. We found a website that was extremely useful and provided very
accurate information and so decided to use it. The website is found at
[https://www.localconditions.com/weather-salt-lake-city-utah/84101/past.php](https://www.localconditions.com/weather-salt-lake-city-utah/84101/past.php)
We decided to begin do a little bit of webscraping to see if we could obtain this information.

Next we will go through a general outline of this process to explain how we were able to obtain this past weather data.


## Process


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Soup.jpg" alt="" style="width:250px;"/>

To begin it is important to know that we used Python and the package called Beautiful Soup to be able to obtain this data. There are of course many different ways to obtain data from websites including web scraping or using APIs. This time I decided to use web scraping as it gave me great practice in deciphering html code and learning more about how websites are set up. We will outline the steps in which we used to obtain this data and good scraping practices we used as well. 

Also, for full code and data visit [my repository](https://github.com/dallinmason/Past-Weather). 

## Steps

### 1. Initial Scrape 
To be able to scrape from any website, we need to establish a connection with it and then obtain the wanted information. I used the requests package in Python to be able to do this and then opened the connection, saved the data into an object, and then closed the connection. 



```
import requests
from urllib.request import urlopen as uReq 


myurl = 'https://www.localconditions.com/weather-salt-lake-city-utah/84101/past.php'

Client = uReq(myurl)
page_html = Client.read()
Client.close()

```

It is excellent web scraping practice to close the connection as soon as you are done with it so that we don't have an open connection forever. This also is courteous to whoever owns the website so that they don't have too many people reading from their website at once which could cause potential problems. 



### 2. Parsing through Data

Our next step will be parsing and sifting through raw html code to be able to decipher what items we want and how we can get them. If you are like me and have not had much experience with html this can be a very tricky step. However, here are some tips to help us do this more efficiently. 

First off we will take a look at the page we have scraped from and the format the data is in. 


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Graph.PNG" alt="" style="width:700px;"/>


So from this we can see that our data comes in a graph like format with all of these variables together. However, we don't want to scrape the wind direction or gust as this doesn't really help us in any way in determining shifts in the seasonal weather patterns as winds can change directions so easily and it could be just telling us where a storm is blowing in or where a front is coming from. 

Therefore, we need to obtain the correct html tags and add this to a dataset.


Using beautiful soup, we can see what information a div tag gives us. 
```
page_soup.findAll("div",{"id":"day1"})

```

<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Sift.PNG" alt="" style="width:700px;"/>


```
containers = page_soup.findAll("table",{"class":"table table-bordered pastwx_grid"})

```














