## 36. our task is to calculate the total cost of admissions for patients based on their insurance status.

Each admission costs $50 for patients without insurance and $10 for patients with insurance. You can determine if a patient has insurance based on their patient_id; all patients with an even patient_id have insurance.

You are required to write a SQL query that does two things:

Label each patient with 'Yes' if they have insurance and 'No' if they don't.
Calculate the total admission cost for each group (Yes and No). Make sure to only use Yes and No strings as labels to pass the tests.
Make sure to set the column names to has_insurance and cost_after_insurance in the sql query to pass the tests

Each admission costs $50 for patients without insurance and $10 for patients with insurance. You can determine if a patient has insurance based on their patient_id; all patients with an even patient_id have insurance.

You are required to write a SQL query that does two things:

Label each patient with 'Yes' if they have insurance and 'No' if they don't.
Calculate the total admission cost for each group (Yes and No). Make sure to only use Yes and No strings as labels to pass the tests.
Make sure to set the column names to has_insurance and cost_after_insurance in the sql query to pass the tests

Concepts Required
Conditional Logic: Use of the CASE statement to apply conditions.
Aggregation: Using SUM to calculate total costs.
Grouping Records: Usage of GROUP BY to segregate data into groups.

<img width="624" height="386" alt="image" src="https://github.com/user-attachments/assets/2e1cb8e7-175b-4186-9c08-0e9f7da0261c" />

###
      SELECT
          CASE
              WHEN patient_id % 2 = 0 THEN 'Yes'
              ELSE 'No'
          END AS has_insurance,
          SUM(CASE
              WHEN patient_id % 2 = 0 THEN 10
              ELSE 50
          END) AS cost_after_insurance
      FROM
          admissions
      GROUP BY
          has_insurance;
###
