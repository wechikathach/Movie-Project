# Blockbuster movie rental data🎥

  
In this notebook, we are going to analyze movie data collected by a movie rental business called Blockbuster. The dataset contains information about the amounts, titles, ratings, and customers. 



1. The company would like to reward the first 10 paying customers. What are the customer ids of the first 10 cusomters who created a payment? 

INPUT:

```sql -- Add 3 backticks followed by sql
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10
``` 
RESULT:

<img width="144" alt="Screen Shot 2022-07-30 at 3 11 33 PM" src="https://user-images.githubusercontent.com/110305874/182001873-9c2e4aa9-d46e-4a65-9485-15b1997962fe.png">



2. A Customer wants to watch 10 movies that is 50 minutes or less. What movies would that be? 

INPUT:

```sql -- Add 3 backticks followed by sql
SELECT title,length from film
where length <=50
LIMIT 10
```
RESULT:

<img width="285" alt="Screen Shot 2022-07-30 at 3 34 45 PM" src="https://user-images.githubusercontent.com/110305874/182002365-9ce75653-7e60-461e-a774-d35f3bca4686.png">


4. A customer would like to know what is the average they will spend to replace a movie for each rating. What is the average replacement cost per MPAA rating? 
INPUT:

```sql -- Add 3 backticks followed by sql
SELECT rating, AVG(replacement_cost)
FROM film
GROUP BY rating
```
RESULT:

<img width="231" alt="Screen Shot 2022-07-31 at 3 23 55 PM" src="https://user-images.githubusercontent.com/110305874/182047688-2711f8ec-7ca5-4971-b452-0caf52004f4c.png">


5. What are the customer ID's of the top 5 customers by total spend? 
INPUT:

```sql -- Add 3 backticks followed by sql
SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5
```

RESULT:

<img width="224" alt="Screen Shot 2022-07-31 at 4 44 32 PM" src="https://user-images.githubusercontent.com/110305874/182050273-38a860a3-dc51-4440-9374-c80ee50fd4ce.png">


6. What customer ID are eligible for platinum status? We are launching a platinum service for our most loyal customers. We will assign platinum status to customer that have 40 or more transactions available? 

INPUT:

```sql -- Add 3 backticks followed by sql
SELECT customer_id, COUNT(*) 
FROM payment
GROUP BY customer_id
HAVING COUNT(*) >= 40;
```
RESULT:

<img width="237" alt="Screen Shot 2022-07-31 at 4 38 16 PM" src="https://user-images.githubusercontent.com/110305874/182050072-6c199cce-72d6-48af-bdcf-8c7e264fd356.png">


7. What customer has the highest customer ID number whose name starts with an ‘E’ and has an address ID lower than 500? 

INPUT:

```sql -- Add 3 backticks followed by sql
SELECT first_name, last_name FROM customer
WHERE first_name like 'E%'
AND address_id <500
ORDER BY customer_id DESC
LIMIT 1;
```
RESULT:

<img width="300" alt="Screen Shot 2022-07-31 at 4 51 58 PM" src="https://user-images.githubusercontent.com/110305874/182050576-113547cf-89fa-4b85-9f29-843b6544a1e4.png">


8. A customer walks in and is a huge fan of the actor “Nick Wahlberg”. They want to know which movies he is in. What are all the movies Nick Wahlberg is in? 

INPUT:

```sql -- Add 3 backticks followed by sql
SELECT title, first_name, last_name
FROM film_actor INNER JOIN actor
ON film_actor.actor_id = actor.actor_id
INNER JOIN film
ON film_actor.film_id = film.film_id
WHERE first_name = ‘Nick’
AND last_name = ‘Wahlberg’
```

RESULT:

<img width="449" alt="Screen Shot 2022-07-31 at 4 50 44 PM" src="https://user-images.githubusercontent.com/110305874/182050539-96eedac9-49cf-4174-ba67-181df77ee626.png">



