#In this SQL, I'm querying a database with multiple tables in it to quantify statistics about customer and order data. 

#1
How many orders were placed in January?
SELECT COUNT (orderid)
FROM BIT_DB.JanSales
WHERE length(orderid) = 6
AND orderid <> 'Order ID'

#2
How many of those orders were for an iPhone?
SELECT COUNT (orderid)
FROM BIT_DB.JanSales
WHERE Product='iPhone'
AND length (orderid) = 6
AND orderid <> 'Order ID'

#3
Select the customers account numbers for all the orders that were placed in February?
SELECT distinct acctnum
FROM BIT_DB.customers cust

INNER JOIN BIT_DB.FebSales Feb
ON cust.order_id = FEB.orderid
WHERE length (orderid)=6
AND orderid <> 'Order ID'

#4
Which product was the cheapest one sold in January, and what was the price?
SELECT distict product, MIN (price)
FROM BIT_DB.JanSales Jan
GROUP BY product,price
ORDER BY price ASC LIMIT 1
#OR
SELECT distinct product, price
FROM BIT_DB.JanSales
WHERE price in (SELECT min(price) FROM BIT_DB.JanSales

#5
What is the total revenue for each product sold in January?
SELECT sum (quantity)*price as revenue
,product
FROM BIT_DB.JanSales
GROUP BY product

#6
Which products were sold in February at 548 Lincoln St,Seattle, WA, 98101, how many of each sold, and what was the total revenue?
SELECT sum(Quantity)
product,
sum(quantity)*price AS revenue
FROM BIT_DB.Febsales
WHERE location = '548 Lincoln St. Seattle, WA, 98101'
GROUP BY product

#7
How many customers ordered more than 2 products at a time in February and what was the average amount spent for these customers?
SELECT 
count (distinct cust. acctnum),
avg (quantity*price)
FROM BIT_DB.customers cust
ON FEB.orderid=cust.order_id
WHERE Feb. Quantity >2
AND length (orderid)=6
AND orderid <> 'Order ID'

##8
SELECT orderdate
FROM BIT_DB.FebSales
WHERE orderdate between '02/13/19 00:00' AND '02/18/19 00:00'

##9 
SELECT location
FROM BIT_DB.FebSales
WHERE orderdate = '02/18/19 01:35'

##10
SELECT sum(quantity)
FROM BIT_DB.FebSales
WHERE orderdate like '02/18/19%'
##11
SELECT distinct Product 
FROM BIT_DB.FebSales
WHERE Product like '%Batteries%'

##12
SELECT distinct Product, Price
FROM BIT_DB.FebSales
WHERE Price like '%.99'


SELECT Product, Sum(quantity)
FROM BIT_DB.FebSales 
WHERE location like '%Los Angeles%'
GROUP BY product


#13 Which locations in New York received at least 3 orders in January, and how many order did they each receive?
SELECT distinct location, count(orderID)
FROM BIT_DB.JanSales 
WHERE location like '%NY%'
AND length (orderid) <> 'Order ID'
GROUP BY location 
HAVING count (orderid) >2

#14 How many of each type of headphone were sold in February?
SELECT sum(quantity) as quantity, product
FROM BIT_DB.FebSales
WHERE product like '%headphone%'
GROUP BY product

#15 What was the average amount spent per account in February?
SELECT sum (quantity*price)/count(cust.acctnum)
FROM BIT_DB.FebSales Feb

LEFT JOIN BIT_DB.customers cust
ON FEB.orderid=cust.order_id

WHERE length(orderid)=6
AND orderid <> 'Order ID'

#16 Which product brought in the most revenue in January and how much revenue did it bring in total?
SELECT product, sum(quantity*price)
FROM BIT_DB.JanSales
GROUP BY product 
ORDER BY sum(quantity*price) desc 
LIMIT 1
