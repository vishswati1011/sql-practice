## 1. Retrieve the track with the longest duration for each genre.

Instructions:

From the "Track" table, fetch the "GenreId" and the name of the track corresponding to the maximum duration for each genre.

Your result should have two columns: "GenreId" and the track's name with the maximum duration, named as "MaxDurationTrackName".

Order your results by "GenreId" in ascending order to ensure consistency in output.

###
      SELECT "GenreId", "Name" as "MaxDurationTrackName"
      from "Track"
      Group By "GenreId"
      having Max("Milliseconds")
      order By "GenreId";
###

## 2. Your task is to identify customers from the Customer table who have never made a purchase. This means they do not have any corresponding records in the Invoice table.

###
      select Customer.FirstName,Customer.LastName from 
      Customer Left join Invoice
      on Customer.CustomerId=Invoice.CustomerId
      where Customer.CustomerId Not in
      (select CustomerId from Invoice )
      Order By Customer.CustomerId;
###


## 3. Determine the number of customers from each country.

###
      select Country , Count(CustomerId) as CustomerCount
      from Customer
      Group By (Country)
      order by Country
###



