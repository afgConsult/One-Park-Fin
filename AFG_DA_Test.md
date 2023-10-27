Alex Francisco Gomez, 
LastUD: 20231026



# Junior Data Analyst Test

This markdown (MD) file will present the answers to the Junior Data Analyst test provided by One Park Financial.

* Question 1: Write a SQL query to get the top 5 deals by funded amount

* Question 2: Write a SQL query to get the total deals and average funded amount by industry.

* Question 3: Build a visual trended view showing funded amount per industry by year and quarter and provide insights on what you see. Include the visual in your answer.

Question 1 and 2 were completely answered in SQL Server Manager Studio (SSMS). Question 3 was answered using SSMS and Excel. 



## Question 1: Write a SQL query to get the top 5 deals by funded amount.

```SQL 
use JR_DA_test;


/* 
Question 1:
Write a SQL query to get the top 5 deals by funded amount
*/

Select TOP (5)	industry_id as 'Industry ID', 
				deal_id as 'Deal Id', 
				funded_amount as 'Funds Amount', 
				funded_date as 'Funded Date'
From dbo.dealTable
order by funded_amount DESC;
```

![Description of the Image](https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q1_results.png?raw=true)



## Question 2: Write a SQL query to get the total deals and average funded amount by industry.


```SQL
/*
Question 2: 
Write a SQL query to get the total deals and average funded amount by industry.
*/
select	dt.industry_id as 'Industry ID', it.industry_name as 'Industry Name',
		count(deal_id) as 'Total Deals',
		avg(funded_amount) as 'Average Funded Amount'
from dbo.dealTable as dt
join dbo.industryTable as it on dt.industry_id = it.industry_id
group by dt.industry_id, it.industry_name
order by dt.industry_id;
```	

![Description of the Image](https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q2_results.png?raw=true)



## Question 3: Build a visual trended view showing funded amount per industry by year and quarter and provide insights on what you see. Include the visual in your answer.


### By Quarter

#### Total Funded Amount by Fiscal Quarter

<img src="https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q3tquart_results.png?raw=true" width=50% height=50%>

* The graph "Total Funded Amount by Fiscal Quarter" has the dollar amount of all Funds along the y axis and the fiscal quarters between 2018 to 2020 along the x axis. 

#### Number of Funds Funded by Fiscal Quarter

<img src="https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q3cquart_results.png?raw=true" width=50% height=50%>

* The graph "Number of Funds by Fiscal Quarter" has the sum of funds accounts opened along the y axis and the fiscal quarters between 2018 to 2020 along the x axis. 

#### Average Funded Amount by Fiscal Quarter

<img src="https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q3quart_results.png?raw=true" width=50% height=50%>

* The graph "Average Funded Amount by Fiscal Quarter" has the average size of a funds account opened for a given quarter along the y axis and the fiscal quarters between 2018 to 2020 along the x axis. 

 
### By Year

#### Total Funded Amount by Year

<img src="https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q3tyear_results.png?raw=true" width=50% height=50%>

* The graph "Total Funded Amount by Year" has the dollar amount of all Funds along the y axis and the years 2018 to 2020 along the x axis. 

#### Number of Funds by Year

<img src="https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q3cyear_results.png?raw=true" width=50% height=50%>

* The graph "Number of Funds by Year" has the sum of funds accounts opened along the y axis and the years 2018 to 2020 along the x axis.  

#### Average Funded Amount by Year

<img src="https://github.com/afgConsult/SampleData/blob/main/jr_da_test_data_q3year_results.png?raw=true" width=50% height=50%>

* The graph "Average Funded Amount by Year" has the average size of a funds account opened for a given year along the y axis and the years 2018 to 2020 along the x axis.   

#### Interpretations

Based on the graphs generated.

* The consitent decline is due to the underperformance of the Q4 2018 - Q3 2019 period followed by the lack of a outlier performance in any of the 2020 quarters staying relatively flat. 

* Funded Amount stayed relativly flat, seeing minial growth or srinkage from Q1 2018 to Q4 2020 on a quater by quarter basis.

* Outlier Funded Amounts by quarters were 2018 Q2 and 2019 Q4.

* Funded Amounts between 2018 to 2020 did not consitantly have above expection performance. Relying on two outlier quarters.

* Fluxuation in the Number of Funds increases starting in 2019 Q3. 

* 2018 Q4 until 2019 Q3 was consitantly below expectations. Lessons learned are best collected in this period.

* Decrease in Funded Amount year over year is consistent with minimal variance.

* Number of Funds is increasing at the same time Total Funds are decreasing.

* Based on the data here and in the quarterly graphs. Average Average Funded Amount plays a larger role in maintaining the Total Funded Amount than the Number of Funds year over year.

* 2019 performed below expectation while 2018 and 2020 performed above expectations when considering Average Funded Amount per Quarter from 2018 Q1 to 2020 Q4.



## Appendix 

### Question 1 and Question 2
DataBase 'JR_DA_test' was created in SSMS to store the 'Deal' and 'Industry' worksheets in the Jr_da_test_data xlsx file.
'dealTable' and 'industryTable' were created in SSMS to store the 'Deal' and 'industry' worksheets respectivly. The syntax below produces the top 5 values of the variable "funded_amount".


### Question 3
The data was wrangled in SSMS by Quarter and by year to obtain data on Average Funded Amounts then imported into Excel using the "Get Data From Text/CSV" into the "sqlimports" tab for graph creation. 
In Excel, within the worksheet "Calculations" a new table was created isolating relvent variables (funded_amount and funded_date) and created variables (year and Fiscal_Quarter). 
The created variables "year" and "Fiscal_Quarter" were created using functions. 
Using the pivot table the graphs for Count and and Total were created.

The Excel function for "Fiscal_Quarter"
```Excel
=IF(AND(C2>=DATE(2020,1,1),C2<=DATE(2020,3,31)),"2020 Q1",
IF(AND(C2>=DATE(2020,4,1),C2<=DATE(2020,6,30)),"2020 Q2",
IF(AND(C2>=DATE(2020,7,1),C2<=DATE(2020,9,30)),"2020 Q3",
IF(AND(C2>=DATE(2020,10,1),C2<=DATE(2020,12,31)),"2020 Q4",
IF(AND(C2>=DATE(2019,1,1),C2<=DATE(2019,3,31)),"2019 Q1",
IF(AND(C2>=DATE(2019,4,1),C2<=DATE(2019,6,30)),"2019 Q2",
IF(AND(C2>=DATE(2019,7,1),C2<=DATE(2019,9,30)),"2019 Q3",
IF(AND(C2>=DATE(2019,10,1),C2<=DATE(2019,12,31)),"2019 Q4",
IF(AND(C2>=DATE(2018,1,1),C2<=DATE(2018,3,31)),"2018 Q1",
IF(AND(C2>=DATE(2018,4,1),C2<=DATE(2018,6,30)),"2018 Q2",
IF(AND(C2>=DATE(2018,7,1),C2<=DATE(2018,9,30)),"2018 Q3",
IF(AND(C2>=DATE(2018,10,1),C2<=DATE(2018,12,31)),"2018 Q4",
"Unknown Quarter"))))))))))))
```

The Excel Function for "Year"
```Excel
=YEAR(Deal!C2)
```


```SQL
/*
Question 3: 
Build a visual trended view showing funded amount per industry by year and quarter and provide insights on what you see. Include the visual in your answer.
*/

drop table dbo.myYearData
drop table dbo.myQuarterData


/* by Quarters */
select
	case
		when funded_date between '2020-01-01' and '2020-03-31' then '2020 Q1' 
		when funded_date between '2020-04-01' and '2020-06-30' then '2020 Q2' 
		when funded_date between '2020-07-01' and '2020-09-30' then '2020 Q3'
		when funded_date between '2020-10-01' and '2020-12-31' then '2020 Q4'

		when funded_date between '2019-01-01' and '2019-03-31' then '2019 Q1'
		when funded_date between '2019-04-01' and '2019-06-30' then '2019 Q2'
		when funded_date between '2019-07-01' and '2019-09-30' then '2019 Q3'
		when funded_date between '2019-10-01' and '2019-12-31' then '2019 Q4'

		when funded_date between '2018-01-01' and '2018-03-31' then '2018 Q1'
		when funded_date between '2018-04-01' and '2018-06-30' then '2018 Q2'
		when funded_date between '2018-07-01' and '2018-09-30' then '2018 Q3'
		when funded_date between '2018-10-01' and '2018-12-31' then '2018 Q4'
		else 'Unknown Quarter'
    end as Quarters,
    round(avg(funded_amount), 2) as 'Average Funded Amount'
into dbo.myQuarterData
from dbo.dealTable
group by
    case
		when funded_date between '2020-01-01' and '2020-03-31' then '2020 Q1' 
		when funded_date between '2020-04-01' and '2020-06-30' then '2020 Q2' 
		when funded_date between '2020-07-01' and '2020-09-30' then '2020 Q3'
		when funded_date between '2020-10-01' and '2020-12-31' then '2020 Q4'

		when funded_date between '2019-01-01' and '2019-03-31' then '2019 Q1'
		when funded_date between '2019-04-01' and '2019-06-30' then '2019 Q2'
		when funded_date between '2019-07-01' and '2019-09-30' then '2019 Q3'
		when funded_date between '2019-10-01' and '2019-12-31' then '2019 Q4'

		when funded_date between '2018-01-01' and '2018-03-31' then '2018 Q1'
		when funded_date between '2018-04-01' and '2018-06-30' then '2018 Q2'
		when funded_date between '2018-07-01' and '2018-09-30' then '2018 Q3'
		when funded_date between '2018-10-01' and '2018-12-31' then '2018 Q4'
		else 'Unknown Quarter'
    end
order by Quarters;


/* by year */
select year(funded_date) as Years, round(avg(funded_amount), 2) as 'Average Funded Amount'
into dbo.myYearData
from dbo.dealTable
group by year (funded_date)
order by Years;
```





