/*This code introduces the LIMIT function */
SELECT occurred_at, account_id, channel
FROM web_events
LIMIT 15;

/*This code introduces ORDERBY */
SELECT id, occurred_at, total_amt_usd
FROM orders ORDER BY occurred_at ;

/*Top 5 orders sorted by total_amt_usd*/
SELECT id, account_id, total_amt_usd
FROM orders ORDER BY total_amt_usd DESC
LIMIT 5;

/*Orderby total the bottom 20 */

SELECT id, account_id, total
From orders ORDER BY total  LIMIT 20 ;

/*Using multiple ORDERBY*/
SELECT * FROM orders
ORDER BY occurred_at DESC, total_amt_usd DESC
LIMIT 5;

SELECT * FROM orders
ORDER BY occurred_at , total_amt_usd
LIMIT 10;

/*introduces WHERE */
SELECT * FROM orders WHERE gloss_amt_usd >= 1000
LIMIT 5;

SELECT * FROM orders WHERE gloss_amt_usd < 500
LIMIT 10;

/*introduces alias*/
SELECT account_id, gloss_qty, poster_qty,
       gloss_qty + poster_qty AS nonstandard_qty

FROM demo.orders;

SELECT id, account_id, standard_amt_usd, standard_qty,
standard_amt_usd/standard_qty
AS unit_price_std FROM orders LIMIT 10;


SELECT id, account_id,
(poster_amt_usd/(standard_amt_usd +gloss_amt_usd+poster_amt_usd))*100
AS percentage_of_revenue FROM orders;

/*introduces LIKE*/
SELECT * FROM demo.web_events_full
WHERE referrer_url like "%google%"

/*Starts with the letter C */
SELECT *
FROM accounts
WHERE name LIKE 'C%';
/*Ends with the letter s */
SELECT *
FROM accounts
WHERE name LIKE '%s';

/*introduces IN*/

SELECT *
FROM demo.orders
WHERE account_id IN (1001, 1021);

SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name IN ('Walmart', 'Target', 'Nordstrom')

Select * from web_events
WHERE channel IN ('organic', 'adwords')
order by channel, account_id;

/* introduces NOT*/
SELECT *
FROM accounts
WHERE name not LIKE 'C%';

/*introduces AND */
SELECT *
FROM demo.orders
WHERE occurred_at >= '2016-04-01' AND occurred_at <= '2016-10-01'
Order by occurred_at DESC

SELECT * FROM orders
where standard_qty > 1000
and poster_qty = 0 and gloss_qty = 0;

/*Using the accounts table find all
the companies whose names do not start
with 'C' and end with 's'.*/
SELECT * FROM accounts
where name not like 'C%' and name like '%s';


/*Use the web_events table to find all information
regarding individuals who were contacted via organic or adwords
and started their account at any point in 2016 sorted from newest to oldest.*/

select *
from web_events where occurred_at
BETWEEN  '2016-1-01' and '2017-1-01'
order by occurred_at desc

/*Find list of orders ids where either gloss_qty or poster_qty
is greater than 4000. Only include the id field in the resulting table.*/
select id, occurred_at from orders
where gloss_qty > 4000 or poster_qty > 4000

/*Write a query that returns a list of orders where
the standard qty is zero and either the gloss
or poster quantity is over 1000.*/
select id from orders
where standard_qty = 0
and (poster_qty > 1000 or gloss_qty >1000)

/*Find all the company names that start with a 'C' or 'W',
and the primary contact contains 'ana' or 'Ana',
 but it doesn't contain 'eana'.*/
 select name, primary_poc from accounts
where (name like 'C%' or name like 'W%')
and (primary_poc like '%ana%' or
     primary_poc like '%Ana%')
and  (primary_poc not like '%eana%');

/*This section is for SQL Joins*/
SELECT orders.*
  FROM demo.orders


SELECT orders.*
FROM orders
JOIN accounts
ON orders.account_id = accounts.id;

/*First JOIN*/
SELECT orders.*, accounts.*
FROM accounts
JOIN orders
ON accounts.id = orders.account_id;
/*************************************/
SELECT orders.standard_qty, orders.gloss_qty,
       orders.poster_qty,  accounts.website,
       accounts.primary_poc
FROM orders
JOIN accounts
ON orders.account_id = accounts.id

/*********************************/
SELECT accounts.name, accounts.primary_poc, web_events.channel
FROM web_events
JOIN accounts
ON web_events.account_id = accounts.id
WHERE accounts.name IN ('Walmart')
/*Using multiple joins*/
FROM web_events
JOIN accounts
ON web_events.account_id = accounts.id
JOIN orders
ON accounts.id = orders.account_id

SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
ORDER BY a.name;

/* More inner Joins*/

SELECT r.name region, a.name account, o.total_amt_usd/(o.total+0.01)  unit
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
JOIN orders o
ON o.account_id = a.id
/*Provide a table that provides the
region for each sales_rep along with their associated
accounts. This time only for the Midwest region.
Your final table should include three columns: the
region name, the sales rep name, and the account name.
Sort the accounts alphabetically (A-Z) according to
account name.*/
SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
WHERE r.name IN ('Midwest')
ORDER BY a.name;
/*Provide a table that provides the region for each
sales_rep along with their associated accounts.
This time only for accounts where the sales rep has a
first name starting with S and in the Midwest region.
Your final table should include three columns: the
region name, the sales rep name, and the account name.
Sort the accounts alphabetically (A-Z) according t
o account name.*/
SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
WHERE r.name IN ('Midwest') and s.name like 'S%'
ORDER BY a.name;

/*Provide a table that provides the region for each
sales_rep along with their associated accounts.
This time only for accounts where the sales rep has a
last name starting with K and in the Midwest region.
Your final table should include three columns: the
region name, the sales rep name, and the account name.
Sort the accounts alphabetically (A-Z) according to
account name.*/
SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
WHERE r.name IN ('Midwest') and s.name like '% K%'
ORDER BY a.name;
/*Provide the name for each region for every order,
as well as the account name and the unit price they paid
(total_amt_usd/total) for the order. However, you should
only provide the results if the standard order quantity
exceeds 100. Your final table should have 3 columns:
region name, account name, and unit price. In order to
 avoid a division by zero error, adding .01 to the
 denominator here is helpful total_amt_usd/(total+0.01)*/
SELECT r.name region, a.name account, o.total_amt_usd/(o.total+0.01)  unit
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty > 100
/*Provide the name for each region for every order, as well as the account name
and the unit price they paid (total_amt_usd/total) for the order. However, you
should only provide the results if the standard order quantity exceeds 100. Your
final table should have 3 columns: region name, account name, and unit price.
In order to avoid a division by zero error, adding .01 to the denominator here
is helpful total_amt_usd/(total+0.01)*/
SELECT r.name region, a.name account, o.total_amt_usd/(o.total+0.01)  unit_price
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty > 100 AND o.poster_qty > 50
ORDER BY unit_price DESC
/*First use of right join*/
SELECT DISTINCT a.name, w.channel
FROM accounts a
RIGHT JOIN web_events w
ON a.id = w.account_id
WHERE a.id = '1001';

/*What are the different channels used by account id 1001.
Your final table should have only 2 columns: account name
and the and the different channels. You can
try SELECT DISTINCT to narrow down the results to
only the unique values*/
SELECT DISTINCT a.name account, w.channel
FROM accounts a
RIGHT JOIN web_events w
ON w.account_id = a.id
where a.id = '1001'

/*Find all the orders that occurred in 2015.
Your final table should have 4 columns: occurred_at,
account name, order total, and order total_amt_usd.*/
SELECT o.occurred_at occured, a.name account,
		o.total total, o.total_amt_usd Dol_Total
FROM accounts a
JOIN orders o
ON o.account_id = a.id
WHERE o.occurred_at
BETWEEN '2015-1-01' AND '2015-12-31'
ORDER BY o.occurred_at ASC
