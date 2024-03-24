# PostgreSQL DVD Rental Database Analysis

## Project Overview

This project analysis and demonstrate the mastery of PostgreSQl queryung technique; 

- Generate Insights
- Complex queries
- Optimize SQL queries


### Data Sources 

The database was gotten from Quantum Analytics NG.
The primary dataset used for this analysis is the " dvdrental.cvs" containing detailed information about Records of the dvd rental company.

### Tools 

- PostgreSQL| Data cleaning and Preparation| Data Anaylsis.


### Data cleaning and preparation

The Tasks:
 1. To load the database and run Locally, follow the step below for postgresql (using Pgadmin)
 2. Unzip the --dvdrental.zip-- file to obtain the --dvdrental.tar--dbfile
 3. Right click on the new database and selsect restore
 4. Select the format under the General tab to **custom or tar**
 5. Select the filename bar and navigate to the file path where the unzipped --dvdrental.tar-- is stored and select it
 6. Click restore and let it load
    

### Exploratory Data Analysis

It involved exploring the data to answer key questions. Such as:

1. How many payment transactions were greater than $5.00
2. How many actors have a first name that starts with the letter p?
3. How many unique districts are our customers from?
4. Retrieve the list of names for those distinct districts from the previous question.
5. How many films have the word Truman somewhere in the title?
6. Create a table to organize our potential leads! We will have the following information: A 
customer's first name, last name, email, sign-up date, and the number of minutes spent on the 
DVD rental site. You should also have some sort of id tracker for them. You have free reign on 
how you want to create this table.
7. What customer has the highest customer ID number whose name starts with an ‘E’ and has an 
address ID lower than 500?
8. Return the customer IDs of customers who have spent at least $110 with the staff member 
who has an ID of 2.
9. How many films have a rating of R and a replacement cost between $5 and $15?
10. What is the maximum payment transaction done by the customer?


### Data Analysis features 

Include some interesting codeworked with 

--  How many payment transactions were greater than $5.00
```Postgresql
SELECT COUNT * FROM PAYMENT
WHERE amount > 5.00;
```

-- How many actions have a first name that starts with the letter p?

```SELECT * FROM actor;
SELECT first_name FROM actor
WHERE first_name LIKE 'P%';
```

--How many unique disricts are our customers from?

```SELECT COUNT(DISTINCT DISTRICT) FROM Address; ```

--Retrive the list of name from those distinct dristicts from the previous question.

```SELECT DISTINCT district FROM address; ```

-- Create a table: customer first_name ,last_name, email,signup date,etc.

```CREATE TABLE customer_details(customer_id SERIAL PRIMARY KEY, customer_first_name VARCHAR (105) NOT NULL, customer_last_name VARCHAR (105) NOT NULL, customer_email VARCHAR (255) UNIQUE NOT NULL, customer_signup_date INT, customer_minutes_on_site INTEGER NOT NULL ); ```


--What customer has the highest customerID number whose name starts with 'E'and has an address ID lower than 500?

```SELECT first_name, last_name,customer_id FROM customer
WHERE first_name LIKE 'E%' AND address_id < 500
ORDER BY customer_id DESC 
LIMIT 1; ```


--Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2.


```SELECT customer_id, staff_id, SUM (amount) FROM PAYMENT
WHERE staff_id = 2
GROUP BY customer_id, staff_id
HAVING sum(amount) >= 110; ```


--How many films have a rating of R and a replacement cost between $5 and $15?

```SELECT count (*) FROM film
WHERE rating = 'R' 
AND replacement_cost BETWEEN 5 AND 15; ```

--what is the maximum payment transcation done by the customer?

```SELECT customer-id MAX(amount)
 FROM payment
GROUP BY customer_id;  ```


