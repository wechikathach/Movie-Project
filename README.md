# Blockbuster movie rental data🎥

  
In this notebook, we are going to analyze movie data collected by a movie rental business called Blockbuster. The dataset contains information about the amounts, titles, ratings, and customers. 

1. The company would like to reward the first 10 paying customers. What are the customer ids of the first 10 cusomters who created a payment? 
```sql -- Add 3 backticks followed by sql
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10
``` 
RESULT:

<img width="144" alt="Screen Shot 2022-07-30 at 3 11 33 PM" src="https://user-images.githubusercontent.com/110305874/182001873-9c2e4aa9-d46e-4a65-9485-15b1997962fe.png">


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

2. A Customer wants to watch 10 movies that is 50 minutes or less. What movies would that be? 
```sql -- Add 3 backticks followed by sql
SELECT title,length from film
where length <=50
LIMIT 10
```
RESULT:
<img width="285" alt="Screen Shot 2022-07-30 at 3 34 45 PM" src="https://user-images.githubusercontent.com/110305874/182002365-9ce75653-7e60-461e-a774-d35f3bca4686.png">

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

CHALLENGE QUESTIONS
3. HOW MANY FILMS HAVE A RATING OF R & A REPLACEMENT COST BETWEEN $5 AND $15? 
Select count(*) from film
where rating='R' and replacement_cost between '5' and '15'


CHALLENGE QUESTION
4. What is the Average replacement cost per MPAA rating? 
SELECT rating, AVG(replacement_cost)
FROM film
GROUP BY rating
"rating"	"avg"
"R"	20.2310256410256410
"PG"	18.9590721649484536
"NC-17"	20.1376190476190476
"PG-13"	20.4025560538116592
"G"	20.1248314606741573

5. What are the customer ids of the top 5 customers by total spend? 
SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5


6. What customer ID are eligible for platinum status? We are launching a platinum service for our most loyal customers. We will assign platinum status to customer that have 40 or more transactions available? 
```sql -- Add 3 backticks followed by sql
SELECT customer_id, COUNT(*) 
FROM payment
GROUP BY customer_id
HAVING COUNT(*) >= 40;
```

7. What are the customer Id of customers who have spent more than 100 in payment transactions with our staff_id member 2? 
SELECT customer_id, SUM(amount) FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) > 100


8. What customer has the highest customer ID number whose name starts with an ‘E’ and has an address ID lower than 500? 
```sql -- Add 3 backticks followed by sql
SELECT first_name, last_name FROM customer
WHERE first_name like 'E%'
AND address_id <500
ORDER BY customer_id DESC
LIMIT 1;
```

9. A customer walks in and is a huge fan of the actor “Nick Wahlberg” and wants to know which movie he is in 
Get a list of all the movies “Nick Wahlberg” has been in. 
```sql -- Add 3 backticks followed by sql
SELECT title, first_name, last_name
FROM film_actor INNER JOIN actor
ON film_actor.actor_id = actor.actor_id
INNER JOIN film
ON film_actor.film_id = film.film_id
WHERE first_name = ‘NICK’
AND last_name = ‘Wahlberg’
```



