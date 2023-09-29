# E-Commerce-Explora-SQL

| ![image](https://github.com/SridharKadhiri/E-Commerce-Explora-SQL/assets/90100318/11b8843f-ebf1-4042-9a97-cfb2e0de8ded) | **Overview**: This README file provides details about the SQL tasks and insights gained from working with the E-Commerce data using MySQL. Below are the tasks performed and the associated SQL commands along with explanations of the insights obtained. |
| ------------- | ------------ |


## Task 1: Creating a New Schema and Importing Data
- Created a new schema named "ecommerce."
- Imported a .csv file named "users_data" into MySQL.

```sql
use ecommerce;
```

## Task 2: Viewing Table Structure
- Checked the structure of the "users_data" table.

```sql
desc users_data;
```

## Task 3: Viewing First 100 Rows
- Displayed the first 100 rows of the "users_data" table.

```sql
select * from users_data limit 100;
```

## Task 4: Counting Distinct Values
- Counted the distinct values for the "country" and "language" fields in the table.

```sql
select count(distinct(country)) Countries, count(distinct(language)) languages from users_data;
```

## Task 5: Identifying Users with Maximum Followers by Gender
- Checked whether male or female users have the maximum number of followers.

```sql
select gender, sum(socialNbFollowers) from users_data group by gender;
```

## Task 6: Analyzing User Behavior
- Investigated various aspects of user behavior, including the use of profile pictures and mobile apps.

```sql
-- 7.(a) Total users who Use Profile Picture in their Profile
select sum(hasProfilePicture = "True" ) from users_data;

-- 7.(b) Total users who Use Application for E-commerce platform
select sum(hasAnyApp = "True") from users_data;

-- 7.(c) Total users who Use Android app
select sum(hasAndroidApp = "True") from users_data;

-- 7.(d) Total users who Use iOS app
select sum(hasIosApp = "True") from users_data;
```

## Task 7: Analyzing Buyer and Seller Data
- Calculated the total number of buyers and sellers for each country and sorted the results.

```sql
-- 8. Calculate the total number of buyers for each country and 
-- sort the result in descending order of total number of buyers.
--  (Consider only those users having at least 1 product bought.)
SELECT 
    COUNT(*) Buyers , country 
FROM
    users_data
WHERE
    productsBought >=1
GROUP BY country
ORDER BY Buyers DESC ;
```

## Task 8: Identifying Top Countries with Maximum Products Pass Rate
- Displayed the names of the top 10 countries with the highest products pass rate.

```sql
select country , productsPassRate from users_data order by productsPassRate desc limit 10;
```

## Task 9: Analyzing User Language Preferences
- Counted the number of users for different language choices.

```sql
select language, count(*) number_of_users  from users_data GROUP BY language;
```

## Task 10: Analyzing Female User Preferences
- Explored female user preferences regarding wishlisting products and liking socially on the e-commerce platform using UNION.

```sql
-- 12. Check the choice of female users about putting the product in a wishlist
--  or to like socially on an ecommerce platform. (Hint: use UNION to answer
--  this question.)
select sum(productsWished) as wishlist_products_to_total_liked, gender from users_data where gender = "F" 
union
select sum(socialProductsLiked), gender from users_data where gender = "F";
```

## Task 11: Analyzing Male User Preferences
- Analyzed male user preferences regarding being sellers or buyers using UNION.

```sql
-- 13. Check the choice of male users about being seller or buyer. (Hint: use UNION 
-- to solve this question.)
select count(gender) Sellers_to_buyers , gender from users_data where gender = "M" and productsSold >= 1
Union
select count(gender) , gender from users_data where gender = "M" and productsBought >= 1;
```

## Task 12: Identifying Countries with Maximum Buyers
- Determined the country with the maximum number of buyers.

```sql
-- 14. Which country is having the maximum number of buyers?
SELECT 
    country ,COUNT(*) Buyers  
FROM
    users_data
WHERE
    productsBought >= 1
GROUP BY country
ORDER BY Buyers DESC limit 1;
```

## Task 13: Identifying Countries with Zero Sellers
- Listed the names of 10 countries with zero sellers.

```sql
-- 15. List the name of 10 countries having zero number of sellers.
SELECT 
    country ,productsSold 
FROM
    users_data
where productsSold = 0
GROUP BY country limit 10;
```

## Task 14: Displaying Recent User Activity
- Displayed records of the top 110 users who have recently used the e-commerce platform.

```sql
-- 16. Display record of top 110 users who have used ecommerce 
-- platform recently.
SELECT 
    *
FROM
    users_data
ORDER BY daysSinceLastLogin
LIMIT 110;
```

## Task 15: Analyzing Inactive Female Users
- Calculated the number of female users who have not logged in for over 100 days.

```sql
-- 17. Calculate the number of female users those who have not 
-- logged in since last 100 days.
SELECT 
    count(*)
FROM
    users_data
WHERE
    daysSinceLastLogin > 100
        AND gender = 'F'; -- 70189
```

## Task 16: Analyzing Female Users by Country
- Displayed the number of female users in each country on the e-commerce platform.

```sql
-- 18. Display the number of female users of each country at ecommerce platform.
SELECT 
    country, COUNT(*) Female_users
FROM
    users_data
where gender = 'F'
GROUP BY country
ORDER BY COUNT(country) DESC;
```

## Task 17: Analyzing Male Users by Country
- Displayed the number of male users in each country on the e-commerce platform.

```sql
-- 19. Display the number of male users of each country at ecommerce platform.
SELECT 
    country, COUNT(country) Male_users
FROM
    users_data
where gender  = "M"
GROUP BY country
ORDER BY COUNT(country) DESC;
```

## Task 18: Analyzing Products Sold and Bought by Male Users
- Calculated the average number of products sold and bought on the e-commerce platform by male users for each country.

```sql
-- 20. Calculate the average number of products sold and bought 
-- on ecommerce platform by male users for each country
SELECT 
    country,
    AVG(productsSold) AvgProductsSoldbyMale,
    AVG(productsBought) AvgProductsBoughtbyMale
FROM
    users_data
WHERE
    gender = 'M'
GROUP BY country
ORDER BY AVG(productsSold) desc, AVG(productsBought);
```

## Conclusion
This README file provides an overview of the tasks performed on the E-Commerce dataset using SQL. Each task is accompanied by the corresponding SQL command and a brief explanation of the insights obtained. The tasks range from data
