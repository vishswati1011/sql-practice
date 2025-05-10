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
