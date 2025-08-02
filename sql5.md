## 37. Show first_name, last_name, and the total number of admissions attended for each doctor. 

admissions (patients_id,admission_Date,discharge_date,attending_doctor_id)

doctors(doctor_id,name)

###
      SELECT doctors.first_name,doctors.last_name,
      count(admissions.attending_doctor_id)
      as admissions_total
      from doctors join admissions
      on doctors.doctor_id=admissions.attending_doctor_id
      group by admissions.attending_doctor_id;
###

## 38. For each day display the total amount of admissions on that day. Display the amount changed from the previous date.
admissions (patients_id,admission_Date,discharge_date,attending_doctor_id)
###
      SELECT
          admission_date,
          COUNT(patient_id) AS admission_day,
          COUNT(patient_id) - LAG(COUNT(patient_id)) OVER (ORDER BY admission_date) AS admission_count_change
      FROM
          admissions
      GROUP BY
          admission_date;
###

## 39. Show the city, company_name, contact_name from the customers and suppliers table merged together. Create a column named "relationship" which contains 'customers' or 'suppliers' depending on the table it came from.

###
      SELECT
          city,
          company_name,
          contact_name,
          'customers' AS relationship
      FROM
          customers
      
      UNION ALL
      
      SELECT
          city,
          company_name,
          contact_name,
          'suppliers' AS relationship
      FROM
          suppliers
      ORDER BY
          city, company_name;
###

## 40. Sort the province names in ascending order in such a way that the province 'Ontario' is always on top

###
      SELECT province_name
      FROM provinces
      ORDER BY
          CASE
              WHEN province_name = 'Ontario' THEN 0 -- Assigns highest priority to Ontario
              ELSE 1                              -- Assigns lower priority to all other provinces
          END,
          province_name ASC;  
###


## 43. You will be tasked with listing the names of albums from the "Album" table that contain tracks in the "Track" table with "UnitPrice" higher than the average unit price across all available tracks.

###
      select Distinct(Album.Title) from Album
      join Track on Album.AlbumId=Track.AlbumId
      where Track.UnitPrice > 
      (Select Avg(UnitPrice) from Track)
      Order By Album.AlbumId;
###
