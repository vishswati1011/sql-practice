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

