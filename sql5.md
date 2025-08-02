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


## 45. You will be tasked with listing the names of albums from the "Album" table that contain tracks in the "Track" table with "UnitPrice" higher than the average unit price across all available tracks.

###
      select Distinct(Album.Title) from Album
      join Track on Album.AlbumId=Track.AlbumId
      where Track.UnitPrice > 
      (Select Avg(UnitPrice) from Track)
      Order By Album.AlbumId;
###

## 46. Task Description: Pivot the Title column from the Employee table into separate columns for each unique title. Count the number of occurrences for each title and display them in separate columns in your output.

Table Used: Employee

Final Columns: Your output should contain the following columns:

SalesAgentCount: Count of employees with the title 'Sales Support Agent'

SupportAgentCount: Count of employees with the title 'Support Representative'

OtherTitleCount: Count of employees with titles not in ('Sales Support Agent', 'Support Representative')

###
      SELECT
          COUNT(CASE WHEN Title = 'Sales Support Agent' THEN 1 END) AS SalesAgentCount,
          COUNT(CASE WHEN Title = 'Support Representative' THEN 1 END) AS SupportAgentCount,
          COUNT(CASE WHEN Title NOT IN ('Sales Support Agent', 'Support Representative') THEN 1 END) AS OtherTitleCount
      FROM
          Employee;
###

## 47.  Identify tracks in the "Track" table that have never been purchased.

Track(TrackId,Name)

InvoiceLine(InvoiceLineId,InvoiceId,TrackId)

###
      Select Track.Name from Track 
      Left join InvoiceLine
      on Track.TrackId=InvoiceLine.TrackId
      where Track.TrackId NOT IN 
      (select TrackId from InvoiceLine);
###

##  48. Write an SQL query to list the top 5 customers who have the highest number of invoices. Your output should show the first names of these customers alongside the count of their invoices.

###
      SELECT Customer.FirstName,
      Count(Invoice.CustomerId) as InvoiceCount
      from Customer join Invoice
      on Customer.CustomerId = Invoice.CustomerId
      Group by Invoice.CustomerId
      Order By InvoiceCount Desc
      Limit 5;
###

## 49. Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)

###
      SELECT
          p.patient_id,
          p.first_name,
          p.last_name
      FROM
          patients AS p
      WHERE
          NOT EXISTS (SELECT 1 FROM admissions AS a WHERE a.patient_id = p.patient_id);
###

## 50. Show all the even numbered Order_id from the orders table using Mod(columnname,n) function.

###
      SELECT
          Order_id
      FROM
          orders
      WHERE
          MOD(Order_id, 2) = 0;
###
