# data-science-independent-project-5

##Additional Challenges

###Intermediate Challenge

What is the percent change 79 in average fare from 2007 to 2017 by flight? How about from 1997 to 2017?
Hint: We can use the WITH clause to create temporary tables containing the airfares, then join them together to compare the change over time.
How would you describe the overall trend in airfares from 1997 to 2017, as compared 2007 to 2017?

###Advanced Challenge

What is the average fare for each quarter? Which quarter of the year has the highest overall average fare? lowest?[^1]

Considering only the flights that have data available on all 4 quarters of the year, which quarter has the highest overall average fare? lowest? Try breaking it down by year as well.[^1]
[^1]: Hint: To consider only flights that have data available for all 4 quarters, we could join the table with itself - each of those tables should be filtered to have data from one quarter.

```sql 
with all_quarter_data (town1, town2, rok) as (
select city1, city2, year
FROM
	airfara
GROUP by
	city1, city2, Year
HAVING count(distinct quarter) = 4
)
select airfara.year, airfara. quarter, avg(airfara.fare)
FROM
	airfara
JOIN
	all_quarter_data
on airfara.city1 = all_quarter_data.town1 and airfara.city2 = all_quarter_data.town2 and airfara.Year = all_quarter_data.rok
group by year, quarter
```
