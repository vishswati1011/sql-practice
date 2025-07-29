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

7. write an SQL query to find patients who have been admitted multiple times for the same diagnosis.

###
    select patient_id, diagnosis 
    from admissions  
    group by patient_id, diagnosis 
    having count(patient_id)>1;
###

8. Your goal is to write a SQL query to show all columns for a patient with a patient_id of 542 based on their most recent admission_date.
   
###
    SELECT * FROM 'admissions' where patient_id=542 group by patient_id having MAX(admission_date);
###

9. write a SQL query that returns the name of each city and the total number of patients residing in that city with the column name as num_patients. Your query should order the results first by the total number of patients (num_patients) in descending order, and then by the city name in ascending alphabetical order.

###
      select city, count(patient_id) as num_patients 
      from patients 
      group by city 
      order by 
          num_patients desc,
          city ASC;
###

10. 

"Artist": Contains artists with columns like "ArtistId" and "Name".

"Album": Stores album information with columns such as "AlbumId", "Title", and "ArtistId".

"Track": Holds track details with columns like "TrackId", "Name", "AlbumId", and others.

"InvoiceLine": Represents invoice lines, and contains columns like "InvoiceLineId", "InvoiceId", "TrackId", "UnitPrice", and "Quantity".



## Objective: Identify and list the top 5 artists based on their total sales.



Tables Involved:

Artist

Album

Track

InvoiceLine

Instructions:

Start by joining the relevant tables to link artists with their sales. The tables to consider are Artist, Album, Track, and InvoiceLine.

## You will need to calculate the total sales for each artist. This involves summing up the product of UnitPrice and Quantity (from InvoiceLine) for tracks associated with each artist.

Sort your results by TotalSales in descending order.

Limit the output to the top 5 results.


## Answer

###
      select ar.Name as ArtistName, 
      sum(iv.UnitPrice * iv.Quantity) as TotalSales 
      from Artist as ar join Album al 
      on ar.ArtistId=al.ArtistId
      join Track as tr 
      on al.AlbumId=tr.AlbumId
      join InvoiceLine as iv
      on tr.TrackId=iv.TrackId
      Group By ar.Name
      Order By TotalSales DESC
      Limit 5;
###
