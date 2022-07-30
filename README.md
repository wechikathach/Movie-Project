# Movie-Project
SELEct * from film
where rental_rate > 4 and replacement_cost >= 19.99;
and rating='R';

ORDER BY
Select column_1, column_2
From table
Order by column_1 ASC/Desc
![image](https://user-images.githubusercontent.com/110305874/181995855-0dfe65e5-4552-4ddd-afec-4a1d17cfade3.png)

Select * from customer
order by first_name asc ;

Select STORE_ID, FIRST_NAME, last_name from customer
order by STORE_ID

LIMIT
Allows the limit of number of rows returned for a query. 
select * from payment 
order by payment_date asc
limit 5;
Top 5 most recent payment dates. 

select * from payment 
where amount !=0.00
order by payment_date asc
limit 5;
Amount is not equal to 0 to find the 5 most recent payments that was not a 0 dollar amount

Customer wants to watch any movie that is 50 minutes or less
select title,length from film
where length <=50

BETWEEN 
BETWEEN low AND high values
Date BETWEEN ‘2007-01-01’ AND ‘2007-01-01’
Note: Pay attention to <=, >=

How many payments are between 8-9 dollars? 
select count(*) from payment
where amount between 8 and 9;

How many payments are NOT between 8-9 dollars? 
select count(*) from payment
where amount not between 8 and 9;
select * from payment
where payment_date between '2007-02-01' and '2007-02-15'

IN 
Use in for a user’s name if its in the list. 
Value IN (option1, option2)
Example
Select color from table
Where color in (‘red,’blue’)

Select color from table
Where color NOT in(‘red,’blue’)

Not jake and john 
select * from customer
where first_name NOT in ('john','jake')

LIKE & ILIKE
WHERE value LIKE ‘Version#__’
-	Cheryl
-	Theresa
-	Sherri
select * from customer
where first_name NOT in ('john','jake')

Select * from customer
where first_name LIKE 'J%' and last_name LIKE 'S%' *ALWAYS USE CAPITAL HOWEVER ILIKE ISNT CAPITAL SENSITIVE

Select * from customer
where first_name LIKE '%er%'
whoever has er in their first name 

CHALLENGE QUESTIONS
HOW MANY FILMS HAVE A RATING OF R & A REPLACEMENT COST BETWEEN $5 AND $15? 
Select count(*) from film
where rating='R' and replacement_cost between '5' and '15'

How many films have the word Truman in the title? 
Select count(*) from film
where title like '%Truman'

HOW MANY ACTORS HAVE THE LETTER P IN THEIR FIRST NAME? 
Select COUNT(*) from actor
Where first_name LIKE ‘P%’

GROUP BY 
Avg()- returns average value
-Can use round to specify after the decimal
Example: SELECT ROUND(AVG(replacement_cost),2)  
From film;
That means rounds to 2 decimal places
Max 
Example: SELECT MAX(replacement_cost) from film
Min 
Example: SELECT MAX(replacement_cost), MIN(replacement_cost)FROM film
Sum- Returns the Sum
Example: SELECT SUM(replacement_cost)
FROM film;
Aggregrate functions happen only in the clause

Categorical columns are non continuous 
Example: SELECT category_col, AGG(data_col) 
FROM table
WHERE category_col !=’A’
GROUP BY category_col
In SELECT statement clumns must either have an aggregate function or be in the GROUP BY call. 
*Group by must appear right after a FROM or WHERE STATEMENT*

SELECT company, division, SUM(sale)
FROM finance_table
GROUP BY company, division

Or WHERE division IN (‘marketing, ‘transport’)
GROUP BY company, division
select Max(replacement_cost), Min(replacement_cost)from film

select Max(replacement_cost), Min(replacement_cost)from film

CHALLENGE QUESTION
What is the Average replacement cost per MPAA rating? 
SELECT rating, AVG(replacement_cost)
FROM film
GROUP BY rating
"rating"	"avg"
"R"	20.2310256410256410
"PG"	18.9590721649484536
"NC-17"	20.1376190476190476
"PG-13"	20.4025560538116592
"G"	20.1248314606741573

What are the customer ids of the top 5 customers by total spend? 
SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5



HAVING LESSON
SELECT company, SUM(sales)
FROM finance_table 
WHERE company !=’Google’
GROUP BY company
HAVING SUM (sales)>1000



SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id   (NOT IN (14)
HAVING SUM(amount) > 100

We cannot use WHERE to filter based off of aggregate results, because those happen after a WHERE is executed 

SELECT store_id, COUNT(customer_id) FROM customer
GROUP BY store_id

Stores that have more than 300 customer
SELECT store_id, COUNT(customer_id) FROM customer
GROUP BY store_id
HAVING count(*) > 300

What customer ID are eligible for platinum status? We are launching a platinum service for our most loyal customers. We will assign platinum status to customer that have 40 or more transactions available? 

SELECT customer_id, COUNT(*) 
FROM payment
GROUP BY customer_id
HAVING COUNT(*) >= 40;



What are the customer Id of customers who have spent more than 100 in payment transactions with our staff_id member 2? 
SELECT customer_id, SUM(amount) FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) > 100



How many films begin with the letter J? 
SELECT count(*) FROM film 
WHERE title LIKE 'J%

What customer has the highest customer ID number whose name starts with an ‘E’ and has an address ID lower than 500? 

SELECT first_name, last_name FROM customer
WHERE first_name like 'E%'
AND address_id <500
ORDER BY customer_id DESC
LIMIT 1;




JOINS LESSON

SELECT amount AS rental_price
FROM payment;
Replaces the amount as the “rental_price”

SELECT SUM(amount) as net_revenue
FROM payment

AS get executed at the END we cannot use it ALIAS or WHERE
Examples where you CANT use it:

SELECT COUNT(amount) AS num_transactions
FROM payment;

SELECT customer_id, SUM(amount) AS total_spent
FROM payment
GROUP BY customer_id
HAVING SUM(amount) > 100 

SELECT customer_id, amount AS new_name
FROM payment
WHERE amount > 2

Inner JOIN lesson will restul with the set of records that match in BOTH tables

SELECT * FROM TableA
INNER JOIN TableB
ON TableA.col_match = TableB. Col_match


SELECT * FROM Registrations 
INNER JOIN Logins
ON Registrations.name = Logins.name

A customer walks in and is a huge fan of the actor “Nick Wahlberg” and wants to know which movie he is in 
Get a list of all the movies “Nick Wahlberg” has been in. 

SELECT title, first_name, last_name
FROM film_actor INNER JOIN actor
ON film_actor.actor_id = actor.actor_id
INNER JOIN film
ON film_actor.film_id = film.film_id
WHERE first_name = ‘NICK’
AND last_name = ‘Wahlberg’

During which months did payments occur? 
SELECT DISTINCT(TO-CHAR(payment_date,’MONTH’))
FROM payment

How many payment occurred on Monday? 
SELECT COUNT(*) 
FROM PAYMENT 
WHERE EXTRACT(dow FROM payment_date)=1

