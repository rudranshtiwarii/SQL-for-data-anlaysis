Questions: MIN, MAX, & AVERAGE
Use the SQL environment below to assist with answering the following questions. Whether you get stuck or you just want to double check your solutions, my answers can be found at the top of the next concept.

Q1 ) When was the earliest order ever placed? You only need to return the date.

ans) 2013-12-04T04:22:44.000Z


Q2 ) Try performing the same query as in question 1 without using an aggregation function.

Query:   SELECT *
         FROM orders
         ORDER BY occurred_at ASC
         
ans) 2013-12-04T04:22:44.000Z

Q3 ) When did the most recent (latest) web_event occur?

Query : SELECT MAX(occurred_at) 
FROM web_events; 

Ans ) 2017-01-01T23:51:09.000Z



Q4) Try to perform the result of the previous query without using an aggregation function.

Query : SELECT *
FROM web_events
ORDER BY occurred_at DESC;

Ans) 2017-01-01T23:51:09.000Z


Q5) Find the mean (AVERAGE) amount spent per order on each paper type, as well as the mean amount of each paper type purchased per order. Your final answer should have 6 values - one for each paper type for the average number of sales, as well as the average amount.

Query : SELECT AVG(standard_amt_usd) mean_standard , AVG(gloss_amt_usd) mean_gloss, AVG(poster_amt_usd) mean_poster, AVG(total_amt_usd) avg_total
FROM orders

Ans) mean_standard	               mean_gloss	                     mean_poster	                     avg_total
     1399.3556915509259259	       1098.5474204282407407	         850.1165393518518519	             3348.0196513310185185
     
   
Q6) Via the video, you might be interested in how to calculate the MEDIAN. Though this is more advanced than what we have covered so far try finding - what is the MEDIAN total_usd spent on all orders?

Query:    SELECT *
          FROM (SELECT total_amt_usd
          FROM orders
          ORDER BY total_amt_usd
          LIMIT 3457) AS Table1
          ORDER BY total_amt_usd DESC
          LIMIT 2;
