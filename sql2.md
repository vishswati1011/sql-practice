
 ## 1. Retrieve the most recent invoice date for every customer in the Chinook database.

you have two table Cutomer and Invoice

cutomer =  cutomerId, name, address
 
Invoice  = invoiceId, customerId, Invoicedate

 ###
      SELECT c.CustomerId, id.InvoiceDate as MaxInvoiceDate from 
      Customer c join Invoice id on
      c.CustomerId = id.CustomerId
      Group By id.CustomerId
      having Max(MaxInvoiceDate)
 ###

## 2. Write an SQL query to display the number of duplicate patients based on their first_name and last_name from patenits table

###
     select 
     first_name,
     last_name,
     count(*) as num_of_duplicates
     from patients 
     Group By first_name, last_name
     having count(*)>1;

###
 
## 3. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000

###
     SELECT * from patients where 
     patient_id IN (1, 45,534,879,1000);
###

## 4. write an SQL query to find the difference between the largest and smallest weight among patients with the last name 'Maroni'.

###
     SELECT Max("weight")-Min("weight") 
     as weight_delta
     from patients 
     where "last_name"='Maroni';

###

## 5. Determine the number of albums associated with each artist in the database.

Two Table we have Artist(ArtistId,Name) Album (albumId,AlbumName,ArtistId)

###
     SELECT
     "Artist"."Name",
     COUNT("Album"."AlbumId") AS "AlbumCount"
     FROM "Artist"
     LEFT JOIN "Album"
       ON "Artist"."ArtistId" = "Album"."ArtistId"
     GROUP BY
       "Artist"."ArtistId",
       "Artist"."Name"
     ORDER BY
       "Artist"."ArtistId";
###

## 6. Identify albums that have tracks missing. For the purpose of this challenge, any album that does not have an associated track in the tracks table is considered to have missing tracks.

You have two Table 
Album(AlbumId,name,ArtistId) 
Track(TrackId, Name,AlbumId)

###
     select "Album"."Title"
     from "Album" left join "Track"
     on "Album"."AlbumId"="Track"."AlbumId"
     where "Album"."AlbumId"  Not IN 
     (Select "TrackId" from "Track" )
     Order By "Album"."AlbumId"
###


## 7. Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name. **Make sure** the column name is `province_name`

you have two table

Patients (patient_id,name,province_id)

Province_names(province_id,province_name)
###

     SELECT
      P.province_name
     FROM patients AS PT
     JOIN province_names AS P
        ON PT.province_id = P.province_id
     GROUP BY
        P.province_id,
        P.province_name
     HAVING
        SUM(CASE WHEN PT.gender = 'M' THEN 1 ELSE 0 END) > SUM(CASE WHEN PT.gender = 'F' THEN 1 ELSE 0 END);
###


## 8. Your challenge is to retrieve the first_name, last_name, and role of every person present in both the patients and doctors tables. You must ensure that the role for each person is correctly labeled as either "Patient" or "Doctor". Make sure to name this column as "role"

you have two tables:

patients (first_name,last_name,patient_id)

doctors(doctor_id,first_name,last_name)

###

     select first_name,last_name,
     'Patient' as "role" from patients
     union all
     select first_name,
     last_name,
     'Doctor' as "role" from doctors; 

###
