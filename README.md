# sql-practice

1. Show `patient_id` and `first_name` from `patients` where their `first_name` start and ends with `s` and is at least `6` characters long and ordered by `patient_id`
   
###
    SELECT patient_id, first_name
    FROM patients
    WHERE first_name LIKE 's%s'
      AND LENGTH(first_name) >= 6
    ORDER BY patient_id;
###


2. Based on cities where our patient lives in, write a query to display the list of unique city starting with a vowel (a, e, i, o, u). Show the result order in ascending by city.

###
    SELECT DISTINCT city
    FROM patients
    WHERE LOWER(SUBSTR(city, 1, 1)) IN ('a', 'e', 'i', 'o', 'u')
    ORDER BY city ASC;
###


3. Show the city, company_name, contact_name of all customers from cities which contains the letter 'L' in the city name, sorted by contact_name

###
    SELECT city, company_name, contact_name
    FROM customers
    WHERE LOWER(city) LIKE '%l%'
    ORDER BY contact_name ASC;
###

4. Show the first_name, last_name, and height of the patient with the greatest height.

###
    SELECT first_name, last_name, height
    FROM patients
    ORDER BY height DESC
    LIMIT 1;
###

5. Show the average unit_price rounded to 2 decimal places as average_price , the total units in stock (use units_in_stock) across all products as total_stock, and the total discontinued products (use discontinued) from as total_discontinued the products table.

###
    SELECT Round(avg(unit_price),2) 
    as average_price, 
    sum(units_in_stock) as total_stock,
    sum(discontinued) as total_discontinued 
    from products;
###

6. Your task is to retrieve a list of artist names (Name) from the Artist table who don't have any associated albums in the Album table. Use the table columns and names provided in the challenge. Your output should consist of artist names (Name), ordered by their ArtistId.

###
    Select name from 
      Artist left join Album 
    on Artist.ArtistId=Album.ArtistId 
    where 
       Album.AlbumId is null
    order by Artist.ArtistId;
###
