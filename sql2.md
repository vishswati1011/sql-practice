# you have two table Cutomer and Invoice

 cutomer =  cutomerId, name, address
 Invoice  = invoiceId, customerId, Invoicedate

 ## Retrieve the most recent invoice date for every customer in the Chinook database.


 ###
      SELECT c.CustomerId, id.InvoiceDate as MaxInvoiceDate from 
      Customer c join Invoice id on
      c.CustomerId = id.CustomerId
      Group By id.CustomerId
      having Max(MaxInvoiceDate)
 ###


2. Write an SQL query to display the number of duplicate patients based on their first_name and last_name from patenits table

###
     select 
     first_name,
     last_name,
     count(*) as num_of_duplicates
     from patients 
     Group By first_name, last_name
     having count(*)>1;

###

3. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000

###
     SELECT * from patients where 
     patient_id IN (1, 45,534,879,1000);
###
