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

   patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.

   attending_doctor_id contains a 2 and the length of patient_id is 3 characters.

SELECT patient_id, attending_doctor_id, diagnosis
FROM admissions
where (patient_id % 2 = 1 and attending_doctor_id in (1,5,19))
      OR (attending_doctor_id LIKE '%2%' AND LEN(patient_id) = 3)

![05](https://github.com/DataRajab/CASE-STUDY-QUESTIONS-AND-INSIGHTS/assets/147069032/ba6d3004-efe4-4632-b3b8-0c173deb5cd4)

6. Show patient_id, first_name, last_name, and attending doctor's specialty.
Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'

SELECT p.patient_id, p.first_name, p.last_name, d.specialty
FROM patients p
join admissions a
on p.patient_id=a.patient_id
join doctors d
on a.attending_doctor_id=d.doctor_id
where a.diagnosis='Epilepsy' and d.first_name = 'Lisa'

![12](https://github.com/DataRajab/CASE-STUDY-QUESTIONS-AND-INSIGHTS/assets/147069032/18ceac76-5f53-404b-9e84-d42d4c20483a)


7. All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.

The password must be the following, in order:
1. patient_id
2. the numerical length of patient's last_name
3. year of patient's birth_date

SELECT distinct p.patient_id, 
       concat(
       p.patient_id,
       len(last_name),
       year(birth_date)
       ) as temp_password
from patients p
join admissions a
on p.patient_id=a.patient_id

![13](https://github.com/DataRajab/CASE-STUDY-QUESTIONS-AND-INSIGHTS/assets/147069032/c49de9ee-addf-4cb2-8b4e-e0985fea7a9d)


8. 
