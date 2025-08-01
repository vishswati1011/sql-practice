# Complex Filtering using Common Table Expressions (CTE)

## We have few table

InvoiceLine(InvoiceLineId ,InvoiceId,TrackId,UnitPrice)

InvoiceId(InvoiceId,CustomerId)

Track(TrackId,Name,AlbumId)

Album(AlbumId,Name)

## To identify invoices that contain more than one track from the same album using Common Table Expressions (CTEs) in the Chinook database, we'll follow these steps:

Join necessary tables: We need to link InvoiceLine to Track and Track to Album to get the AlbumId for each invoice line.

Count tracks per album per invoice: For each InvoiceId and AlbumId, count how many TrackId entries exist.

Filter for duplicates: Identify the InvoiceId and AlbumId combinations where the count of tracks is greater than 1.

Count duplicate albums per invoice: For each InvoiceId, count how many distinct AlbumIds had more than one track.


###

      WITH InvoiceAlbumTracks AS (
          SELECT
              il.InvoiceId,
              t.AlbumId,
              COUNT(il.TrackId) AS TrackCount
          FROM
              InvoiceLine AS il
          JOIN
              Track AS t
              ON il.TrackId = t.TrackId
          GROUP BY
              il.InvoiceId,
              t.AlbumId
      ),
      DuplicateAlbumsPerInvoice AS (
          SELECT
              InvoiceId,
              COUNT(AlbumId) AS DuplicateAlbumCount
          FROM
              InvoiceAlbumTracks
          WHERE
              TrackCount > 1
          GROUP BY
              InvoiceId
      )
      SELECT
          InvoiceId,
          DuplicateAlbumCount
      FROM
          DuplicateAlbumsPerInvoice
      ORDER BY
          InvoiceId;


###
