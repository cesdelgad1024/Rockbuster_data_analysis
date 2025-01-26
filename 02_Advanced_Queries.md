## **Group B: Advanced Queries**  
These queries focus on advanced SQL techniques, such as CTEs, subqueries, window functions, and case statements.

#### **1. Window Functions**  
SELECT customer_id,   
       SUM(amount) AS total_spent,   
       RANK() OVER (ORDER BY SUM(amount) DESC) AS rank  
FROM payment  
GROUP BY customer_id  
LIMIT 10;  
<sub>_This query ranks the top 10 customers based on total payments made._<sub/>

#### **2. Subqueries**  
##### Example 1: Customer Count by Country  
SELECT country, COUNT(customer_id) AS total_customers  
FROM (  
    SELECT cu.customer_id, co.country  
    FROM customer cu  
    INNER JOIN address ad ON cu.address_id = ad.address_id  
    INNER JOIN city ci ON ad.city_id = ci.city_id  
    INNER JOIN country co ON ci.country_id = co.country_id  
) AS country_customers  
GROUP BY country  
ORDER BY total_customers DESC  
LIMIT 10;  
<sub>_This query identifies the top countries with the highest customer count using a subquery._<sub/>

##### Example 2: Filtering Top Cities within Countries  
SELECT city_id, COUNT(customer_id) AS total_customers  
FROM customer  
WHERE country_id IN (  
    SELECT country_id  
    FROM customer  
    GROUP BY country_id  
    HAVING COUNT(customer_id) > 50  
)  
GROUP BY city_id  
ORDER BY total_customers DESC  
LIMIT 10;  
<sub>_This query filters and retrieves top cities in countries with more than 50 customers._<sub/>

#### **3. CTEs (Common Table Expressions)**  
##### Example 1: Multi-step Aggregation  
WITH top_countries AS (  
    SELECT country_id, COUNT(customer_id) AS total_customers  
    FROM customer  
    GROUP BY country_id  
    ORDER BY total_customers DESC  
    LIMIT 10  
),  
top_cities AS (  
    SELECT city_id, COUNT(customer_id) AS total_customers  
    FROM customer  
    WHERE country_id IN (SELECT country_id FROM top_countries)  
    GROUP BY city_id  
    ORDER BY total_customers DESC  
    LIMIT 10  
)  
SELECT city_id, SUM(amount) AS total_payments  
FROM payment  
WHERE city_id IN (SELECT city_id FROM top_cities)  
GROUP BY city_id  
ORDER BY total_payments DESC;  
<sub>_This query calculates total payments for the top cities in the top countries using CTEs._<sub/>  

##### Example 2: Summarized Payment Analysis  
WITH customer_payments AS (  
    SELECT customer_id, SUM(amount) AS total_amount  
    FROM payment  
    GROUP BY customer_id  
)  
SELECT customer_id, total_amount  
FROM customer_payments  
WHERE total_amount > 100;  
<sub>_This query summarizes payment data and filters customers who spent more than $100._<sub/>

#### **4. Complex Query with Case Statements**
SELECT f.title,  
       CASE   
           WHEN f.rental_rate > 4 THEN 'Premium'  
           WHEN f.rental_rate BETWEEN 2 AND 4 THEN 'Standard'  
           ELSE 'Budget'  
       END AS rental_category  
FROM film f;  
<sub>_This query categorizes films into Premium, Standard, or Budget based on their rental rate.<sub/>
