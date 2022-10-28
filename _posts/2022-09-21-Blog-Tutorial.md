---
layout: post
title:  "A Rosetta Stone for Merging Tables"
date:   2022-09-21
author: Dallin Mason
description: An excellent tutorial on the syntax differences between merging tables in R vs. SAS
image: /assets/images/Rosetta_Stone.JPG
---

# A Rosetta Stone for Merging Tables



For those of us who are further advanced along our programming knowledge and have dabbled in a few of the statistical coding languages, keeping track of syntax can be a nightmare! It seems like as soon as you get in the mindset of one language, the next one is out the window again! 

How can we fix this??

The goal of this tutorial is to help us keep track of how R and SAS use different commands to do the same thing, merge two tables together.


## Merging
Most, if not all of you, have probably encountered situations where two statistical tables become necessary to join in order to compute accurate results about a certain set of data. The easiest way to do this is to merge them together using the language you are manipulating the data in. 


Among the most common used languages in statistics is R and so you may find yourself using this language in your career if you have not used it before. Another less common programming language is SAS which usually takes a license to use so most people, unless in a healthcare industry, will not use SAS. However, for those who might eventually use it, I have chosen to compare SAS and R in this tutorial and show the differences between merging two tables in these languages.

We will start with going through the basics of merging in R. 

## R Merging



<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/R.png" alt="" style="width:100px;"/>



 
 
We will go through the different merges with examples of how to do so. I will start with using a dataset that compares different acclaimed universities and their counts of statistical undergraduates per year. 

### Code:

```
stat_programs <- read_csv("data.csv")
```
For the data visit this [link](https://raw.githubusercontent.com/dallinmason/stat386-projects/main/data.csv). 
I read in the data using read_csv. For more information on read_csv and how this works in reading in data efficiently visit this website on [read_csv](https://r4ds.had.co.nz/data-import.html). 
### Table: 
<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Table1_Pic.PNG" alt="" style="width:250px;"/>


We will merge this table with that comparing these same schools and the amount of Nobel Peace Prizes that have been awarded to that school during that respective year.

### Code:
```
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
```

  
### Table: 
<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/T2.PNG" alt="" style="width:250px;"/>







First off we consider a scenario where we want to look at the table of statistical undergraduates but add the Nobel Peace Prize count per year column to this table. To do this we will use a left join as shown:

```
stat_programs%>%
  left_join(school_tuition,by=c("School","Year"))
 ``` 
  
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
```
stat_programs%>%
  inner_join(school_tuition,by=c("School","Year"))
```  
  
  
### Table: 


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Inner_Join.PNG" alt="" style="width:250px;"/>




So as you can see, it is not too complicated to merge tables together in R. But what if you want to perform the same commands in SAS?

## SAS


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/SAS.webp" alt="" style="width:250px;"/>


We will now demonstrate the same functions that we executed in R but now for SAS. The interesting thing about SAS is that to be able to perform merging operations we actually use SQL syntax that SAS understands and then it converts what we tell it to do into SAS formatted tables. So if you master these SQL commands we use in SAS you will actually be set to do the same in SQL! It's a two for one bonus! 

To demonstrate this we will use a different couple of datasets in which there are certain employees of varying positions and we have certain data about them including their past sales over the past years.

We will demonstrate our knowledge of SAS and SQL with these datasets. 

We will import our tables using this code which creates two tables: one of employees with information about them and another called employees_s which demonstrates the sales per month of these employees.

## Code
```
options validvarname=v7;
proc import datafile="/home/u49683781/EPG1V2/Assignment_work/employees.xlsx" out= employees dbms=xlsx replace;
run;
proc import datafile="/home/u49683781/EPG1V2/Assignment_work/employees_sales.xlsx" out=employees_s dbms=xlsx replace;
run;
```

## Tables

<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Table1_SAS.PNG" alt="" style="width:250px;"/>


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Table2_SAS.PNG" alt="" style="width:250px;"/>


First, we will start with our left join.

## Code
```
*proc sql to combine tables;
proc sql;
select employees.name, age, position, group, state, month, sales, year
	from employees as x left join employees_s as y
	on x.name=y.name;
 ```

We simply import these files and then pipe this all through proc sql which is such a huge advantage of SAS. 






## Table


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Left_Join_SAS.PNG" alt="" style="width:250px;"/>

So as you can see, the left join executed well. There is a little bit of difference from R as you can see but it is not too terrible to be able to follow the syntax and reproduce these tables and even make adjustments to them as will be demonstrated with our next example.

That is that of a right join in SAS. 

## Code
```
proc sql;
select employees.name, age, position, group, state, month, sales, year
	from employees as x right join employees_s as y
	on x.name=y.name;
```




## Table


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Right_Join_SAS.PNG" alt="" style="width:250px;"/>


As you can see we literally only changed one word. So that is very simple and easy to mess around with.

Finally we will demonstrate how to use an inner join using SAS.


## Code
```
proc sql;
select employees.name, age, position, group, state, month, sales, year
	from employees as x inner join employees_s as y
	on x.name=y.name;
```



## Table


<img src="https://raw.githubusercontent.com/dallinmason/stat386-projects/main/assets/images/Inner_Join_SAS.PNG" alt="" style="width:250px;"/>

So as you can see. SAS is not that hard to mess around with, it just takes a little getting familiar with the syntax. 

Overall, we can see the differences between R and SAS and how both are beneficial in merging datasets it just takes familiarizing oneself with how to do it in these specific languages. One suggestion I have been counseled to do and I pass it along to you is to create some sort of documentation where you can reference how to do similar commands in different programming environments so as to avoid confusion! It will help you become a more efficient programmer over time!


For more information about these topics I have provided a couple of websites I find helpful.



* [https://www.listendata.com/2014/06/proc-sql-merging.html](https://www.listendata.com/2014/06/proc-sql-merging.html) 
* [https://www.rdocumentation.org/packages/plyr/versions/1.8.7/topics/join](https://www.rdocumentation.org/packages/plyr/versions/1.8.7/topics/join)
* [https://rforhr.com/join.html](https://rforhr.com/join.html)
