# sql-practice

1. Based on cities where our patient lives in, write a query to display the list of unique city starting with a vowel (a, e, i, o, u). Show the result order in ascending by city.

###
    SELECT DISTINCT city
    FROM patients
    WHERE LOWER(SUBSTR(city, 1, 1)) IN ('a', 'e', 'i', 'o', 'u')
    ORDER BY city ASC;
###
