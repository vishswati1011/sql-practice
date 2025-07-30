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
