# Rockbuster Data Dictionary

### Author: Cesar S. Delgado
**Date**: January 19, 2025

**Purpose**: This document serves as the official data dictionary for the Rockbuster database. It provides detailed information about the fact and dimension tables, including their attributes, primary keys, foreign keys, and relationships.

---

## Table of Contents
1. Summary of Fact and Dimension Tables
2. Fact Tables
   - Payment Table
   - Rental Table
3. Dimension Tables
   - Inventory Table
   - Film Table
   - Actor Table
   - Film Actor Table
   - Category Table
   - Film Category Table
   - Customer Table
   - Staff Table
   - Store Table
   - Address Table
   - City Table
   - Country Table
   - Language Table
4. Relationships and Keys
5. SQL Insights and Analysis
   - Film Table Summary
   - Top 10 Movies by Revenue
   - Revenue by Country
   - Top 5 Customers in Top Cities
   - Category Frequency

---

## 1. Summary of Fact and Dimension Tables

### Fact Tables:
- **Payment**: Contains monetary transaction details.
- **Rental**: Contains rental transaction details.

### Dimension Tables:
- Inventory, Film, Actor, Film Actor, Category, Film Category
- Customer, Staff, Store, Address, City, Country, Language

---

## 2. Fact Tables

### Payment Table
| Column Name   | Data Type        | Description                       |
|---------------|------------------|-----------------------------------|
| `payment_id`  | SERIAL (PK)      | Surrogate PK for payment.         |
| `customer_id` | SMALLINT (FK)    | FK to customer.                   |
| `staff_id`    | SMALLINT (FK)    | FK to staff.                      |
| `rental_id`   | INTEGER (FK)     | FK to rental.                     |
| `amount`      | NUMERIC(5, 2)    | Payment amount.                   |
| `payment_date`| TIMESTAMP(6)     | When payment was made.            |

### Rental Table
| Column Name   | Data Type        | Description                       |
|---------------|------------------|-----------------------------------|
| `rental_id`   | SERIAL (PK)      | Surrogate PK for rental.          |
| `rental_date` | TIMESTAMP(6)     | When rental began.                |
| `inventory_id`| INTEGER (FK)     | FK to inventory.                  |
| `customer_id` | SMALLINT (FK)    | FK to customer.                   |
| `return_date` | TIMESTAMP(6)     | When rental was returned.         |
| `staff_id`    | SMALLINT (FK)    | FK to staff.                      |
| `last_update` | TIMESTAMP(6)     | Last update timestamp.            |

---

## 3. Dimension Tables

### Inventory Table
| Column Name   | Data Type        | Description                       |
|---------------|------------------|-----------------------------------|
| `inventory_id`| SERIAL (PK)      | Surrogate PK for inventory.       |
| `film_id`     | SMALLINT (FK)    | FK to film.                       |
| `store_id`    | SMALLINT (FK)    | FK to store.                      |
| `last_update` | TIMESTAMP(6)     | Last update timestamp.            |

### Film Table
| Column Name      | Data Type            | Description                       |
|------------------|----------------------|-----------------------------------|
| `film_id`        | SERIAL (PK)          | Surrogate PK for film.            |
| `title`          | VARCHAR(255)         | Film title.                       |
| `description`    | TEXT                 | Film description.                 |
| `release_year`   | YEAR                 | Year released.                    |
| `language_id`    | SMALLINT (FK)        | FK to language.                   |
| `rental_duration`| SMALLINT             | Days allowed for rental.          |
| `rental_rate`    | NUMERIC(4, 2)        | Rental cost.                      |
| `length`         | SMALLINT             | Film length (minutes).            |
| `replacement_cost`| NUMERIC(5, 2)       | Replacement cost.                 |
| `rating`         | CHAR(5)              | MPAA rating.                      |
| `last_update`    | TIMESTAMP(6)         | Last update timestamp.            |

... *(Additional dimension tables follow the same format as above.)*

---

## 4. Relationships and Keys
- **Film -> Language**: The film table is linked to the language table via the `language_id` column.
- **Film Actor -> Film**: The film_actor table is linked to the film table via the `film_id` column.
- **Payment -> Rental**: The payment table is linked to the rental table via the `rental_id` column.
- **Payment -> Customer**: Links a customer’s details for payment transactions.
- **Address -> City**: The address table is linked to the city table via the `city_id` column.
- **City -> Country**: The city table is linked to the country table via the `country_id` column.
- **Category -> Film Category**: The category table is linked to the film_category table via the `category_id` column.

---

## 5. SQL Insights and Analysis

### Film Table Summary
| Metric               | Value             |
|----------------------|-------------------|
| Min Release Year     | 2006              |
| Max Release Year     | 2006              |
| Avg Release Year     | 2006              |
| Min Rental Duration  | 3                 |
| Max Rental Duration  | 7                 |
| Avg Rental Duration  | 5                 |
| Min Rental Rate      | 0.99              |
| Max Rental Rate      | 4.99              |
| Avg Rental Rate      | 2.99              |
| Min Replacement Cost | 9.99              |
| Max Replacement Cost | 29.99             |
| Avg Replacement Cost | 19.99             |

### Top 10 Movies by Revenue
| Movie Title        | Total Revenue      |
|--------------------|--------------------|
| Telegraph Voyage   | $215.75M           |
| Zorro Ark          | $199.72M           |
| Wife Turn          | $198.73M           |

... *(Include additional insights as per your document.)*
