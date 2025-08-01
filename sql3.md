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

