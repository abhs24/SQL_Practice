**https://www.sql-practice.com/**

Inner Join with comman columnn
SELECT* from patients INNER join admissions on patients.patient_id=admissions.patient_id;


To find Null or Not null keys

SELECT* from patients where allergies is NOT  NULL;


//Q:Show unique birth years from patients and order them by ascending.
SELECT DISTINCT YEAR(birth_date) AS birth_year from patients order by  birth_year

Show first name and last name concatinated into one column to show their full name.
SELECT CONCAT(first_name, ' ', last_name) AS full_name

//Q:Show first name and last name concatinated into one column to show their full name.
select concat(first_name,' ',last_name)As FullName from patients

//Q:Show first name, last name, and the full province name of each patient.
//Example: 'Ontario' instead of 'ON'
select p.first_name,p.last_name,r.province_name
from patients p inner join  province_names r
on p.province_id=r.province_id


//Q:Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
SELECT patient_id,first_name FROM patients where first_name like 's____%s'//4spaces & 1st,lasst name is S


//Q:Show all columns for patients who have one of the following patient_ids:1,45,534,879,1000
SELECT * FROM patients where patient_id IN (1,45,534,879,1000)


//Q:Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.

SELECT p.patient_id,p.first_name,p.last_name  from patients p join admissions a 
on p.patient_id=a.patient_id
where a.diagnosis='Dementia'

//Q:Display every patient's first_name.Order the list by the length of each name and then by alphabetically.
SELECT first_name
FROM patients
ORDER BY LENGTH(first_name), first_name;

//Q:Show the total number of admissions
SELECT count(patient_id)As total_admission FROM admissions

//Q:Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.

SELECT
  SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) AS male_count,
  SUM(CASE WHEN gender='F' THEN 1 Else 0 end) As female_count
  from patients

//Q.Show all the columns from admissions where the patient was admitted and discharged on the same day.
SELECt * from admissions where admission_date=discharge_date;

//Q.Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.
Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

//Q.Show unique first names from the patients table which only occurs once in the list.

For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.

SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(*) = 1;

//Q.Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.
Ans:select patient_id,diagnosis from admissions
group by patient_id,diagnosis
having count(*)>1


//Q:Show the patient id and the total number of admissions for patient_id 579.

SELECT patient_id, COUNT(*) AS total_admissions
from admissions
where patient_id=579

//Q.Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.

SELECT
    city,
    COUNT(*) AS total_patients
FROM
    patients
GROUP BY
    city
ORDER BY
    total_patients DESC,
    city ASC;
	
//Q:Show first name, last name and role of every person that is either patient or doctor.
The roles are either "Patient" or "Doctor"

SELECT first_name, last_name, 'Patient' AS role 
FROM patients
UNION ALL
SELECT first_name, last_name, 'Doctor' AS role 

FROM doctors;
//

Q.**Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.**
A->SELECT province_id, SUM(height) FROM patients GROUP BY province_id HAVING SUM(height) >= 7000

Q.**Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.**
A->select first_name,last_name,birth_date  from patients where Year(birth_date) between 1970 and 1979
order by birth_date ASC;

