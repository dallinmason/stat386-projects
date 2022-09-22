---
layout: post
title:  "The Rosetta Stone of Merging Tables"
date:   2022-09-21
author: Dallin Mason
description: A tutorial on the differences between R and SAS
image: /assets/images/Rosetta_Stone.JPG
---

# The Rosetta Stone of Merging Tables



For those of us who are further advanced along our programming knowledge and have dabbled in a few of the statistical coding languages, keeping track of syntax can be a nightmare! It seems like as soon as you get in the mindset of one language, the next one is out the window again! 

How can we fix this??

The goal of this tutorial is to help us keep track of how R and SAS use different commands to do the same thing, merge two tables together.


## Merging
Most, if not all of you, have probably encountered situations where two statistical tables become necessary to join in order to compute accurate results about a certain set of data. The easiest way to do this is to merge them together using the language you are manipulating the data in. 


Among the most common used languages in statistics is R and so you may find yourself using this language in your career if you have not used it before. Another less common programming language is SAS which usually takes a license to use so most people, unless in a healthcare industry, will not use SAS. However, for those who might eventually use it, I have chosen to compare SAS and R in this tutorial and show the differences between merging two tables in these languages.

We will start with going through the basics of merging in R. 

<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/R.png" alt="" style="width:100px;"/>


## R Merging
 
 
We will go through the different merges with examples of how to do so. I will start with using a dataset that compares different acclaimed universities and their counts of statistical undergraduates per year. 

### Code:

stat_programs <- read_csv("
School, Year, BS_Stat
Berkeley, 2013, 143
Berkeley, 2014, 160
Berkeley, 2015, 215
Berkeley, 2016, 174
Berkeley, 2017, 215
Berkeley, 2018, 226
BYU, 2013, 35
BYU, 2014, 42
BYU, 2015, 57
BYU, 2016, 69
BYU, 2017, 101
BYU, 2018, 136
Duke, 2013, 8
Duke, 2014, 14
Duke, 2015, 23
Duke, 2016, 33
Duke, 2017, 40
Duke, 2018, 33
Harvard, 2013, 23
Harvard, 2014, 36
Harvard, 2015, 43
Harvard, 2016, 63
Harvard, 2017, 95
Harvard, 2018, 100
")


### Table: 
<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Table1_Pic.PNG" alt="" style="width:250px;"/>


We will merge this table with that comparing these same schools and the amount of Nobel Peace Prizes that have been awarded to that school during that respective year.

### Code:
school_nobel <- read_csv("
School, Year, Nobel
Harvard, 2013, 5
Harvard, 2014, 1
Harvard, 2016, 3
Harvard, 2018, 1
Harvard, 2019, 4
Berkeley, 2013, 1
Berkeley, 2014, 1
Berkeley, 2015, 2
Berkeley, 2016, 1
Berkeley, 2017, 3
Berkeley, 2018, 2
Duke, 2015, 1
Duke, 2018, 1
Duke, 2019, 1
")

  
### Table: 
<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/T2.PNG" alt="" style="width:250px;"/>


First off we consider a scenario where we want to look at the table of statistical undergraduates but add the Nobel Peace Prize count per year column to this table. To do this we will use a left join as shown:


stat_programs%>%
  left_join(school_tuition,by=c("School","Year"))
  
  
<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Left_Join.PNG" alt="" style="width:250px;"/>

Now we will consider the opposite situation where we want to match up the various years schools got Nobel Peace Prizes and exclude the years that they did not. To do this we will use a right join as follows:


### Code:

```
stat_programs%>%
  right_join(school_tuition,by=c("School","Year"))
``` 
  
### Table:


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Right_Join.PNG" alt="" style="width:250px;"/>



Finally we will consider a situation where you would like to find out where this data matches up without any wholes or missing values. To do this we will use an inner join:

### Code:

stat_programs%>%
  inner_join(school_tuition,by=c("School","Year"))
  
  
  
### Table: 


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Inner_Join.PNG" alt="" style="width:250px;"/>
