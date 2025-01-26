## **Basic and Intermediate Queries**  
These queries cover foundational concepts like SELECT, filtering, grouping, joins, and data cleaning.
---
#### **1. Basic SELECT and Filtering:**  

SELECT rental_duration AS "rented for (in days)", COUNT(*) AS "number of films"  
FROM film  
GROUP BY rental_duration  
ORDER BY COUNT(*) DESC;    
<sub>_This query shows the distribution of films based on rental duration_</sub>



#### **2. Aggregation and Grouping:**    
SELECT MIN(replacement_cost) AS min_cost,          
       MAX(replacement_cost) AS max_cost,          
       AVG(replacement_cost) AS avg_cost           
FROM film;                                       
<sub>_This query provides the minimum, maximum, and average replacement cost of films._<sub/>


#### **3. Joins:**  
##### Example 1: Basic Join with Filtering  
SELECT f.title, c.name AS category, a.first_name, a.last_name  
FROM film f  
INNER JOIN film_category fc ON f.film_id = fc.film_id  
INNER JOIN category c ON fc.category_id = c.category_id  
INNER JOIN film_actor fa ON f.film_id = fa.film_id  
INNER JOIN actor a ON fa.actor_id = a.actor_id  
WHERE c.name = 'Action';  
<sub>_This query retrieves films categorized as 'Action' along with actor details._<sub/>


##### Example 2: Join for Geographic Insights
SELECT co.country, COUNT(cu.customer_id) AS customer_count  
FROM customer cu  
INNER JOIN address ad ON cu.address_id = ad.address_id  
INNER JOIN city ci ON ad.city_id = ci.city_id  
INNER JOIN country co ON ci.country_id = co.country_id  
GROUP BY co.country  
ORDER BY customer_count DESC  
LIMIT 10;  
<sub>_This query identifies the top 10 countries with the highest number of customers._<sub/>


#### **4. Data Cleaning:**  
UPDATE customer  
SET email = TRIM(email),  
    first_name = INITCAP(first_name),  
    last_name = INITCAP(last_name)  
WHERE email IS NOT NULL;  
<sub>_This query standardizes customer data by cleaning and formatting names and emails._<sub/>
