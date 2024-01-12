# SQL-Practice-Questions
A. TABLE DATA EXPLORATION

1. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.

SELECT province_id, sum(height)
FROM patients
group by province_id
having sum(height) >= 7000

![01](https://github.com/DataRajab/CASE-STUDY-QUESTIONS-AND-INSIGHTS/assets/147069032/923988da-9e78-4d1f-bfef-3e008f95f6db)

2. Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'

SELECT max(weight)-min(weight) as weight_difference
FROM patients
WHERE last_name = 'Maroni';

![02](https://github.com/DataRajab/CASE-STUDY-QUESTIONS-AND-INSIGHTS/assets/147069032/c9531dd8-17ff-4d32-99ca-3c61d060b985)

3. Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.

SELECT day(admission_date) AS DAY, count(*) as num_of_occurrence
FROM admissions
group by day(admission_date)
order by num_of_occurrence DESC

![03](https://github.com/DataRajab/CASE-STUDY-QUESTIONS-AND-INSIGHTS/assets/147069032/bb697a28-5225-4d20-99fb-7200b792d97f)

4. Show all columns for patient_id 542's most recent admission_date.

SELECT *
FROM admissions
where patient_id = 542
order by admission_date desc
limit 1

![04](https://github.com/DataRajab/CASE-STUDY-QUESTIONS-AND-INSIGHTS/assets/147069032/db835fa4-981c-4281-a5c0-df14b95f7d7d)

5. Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:
1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.

SELECT patient_id, attending_doctor_id, diagnosis
FROM admissions
where (patient_id % 2 = 1 and attending_doctor_id in (1,5,19))
      OR (attending_doctor_id LIKE '%2%' AND LEN(patient_id) = 3)
