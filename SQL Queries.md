-- select
	max(num_of_visits) as max_visits,
	min(num_of_visits) as min_visits,
    round(avg(num_of_visits), 2) as avg_visits
from (
  select count(*) as num_of_visits
  from admissions
  group by admission_date
)



-- select patient_id, first_name, last_name from patients
WHERE patients.patient_id not in (
	select patient_id from admissions
)
-- select
	concat(first_name, ' ', last_name) as full_name,
	ROUND(height / 30.48, 1) as 'height "Feet"',
    ROUND(weight * 2.205, 0) as 'weight "Pound"',
    birth_date,
    case
      when gender = 'M' then 'Male'
      when gender = 'F' then 'Female'
      else gender
    end as gender
from patients;


-- select first_name, last_name, count(concat(first_name, " ", last_name)) as num_of_duplicates
from patients
group by
	concat(first_name, " ", last_name)
having
    num_of_duplicates > 1;

-- select concat(patients.first_name, " ", patients.last_name) as patients_full_name, admissions.diagnosis, concat(doctors.first_name, " ", doctors.last_name) as doctors_full_name
from admissions
	join doctors on admissions.attending_doctor_id = doctors.doctor_id
	join patients on admissions.patient_id = patients.patient_id


-- select province_names.province_name, count(*) as patient_count from patients join province_names on patients.province_id = province_names.province_id group by province_name order by patient_count desc;
-- 18
-- select doctors.doctor_id, concat(doctors.first_name, " ", doctors.last_name) as full_name, min(admissions.admission_date) as first_admission_date, max(admissions.admission_date) as last_admission_date from doctors join admissions on admissions.attending_doctor_id = doctors.doctor_id group by doctors.doctor_id;
-- select doctors.first_name, doctors.last_name, count(*) as total_number_of_admission from admissions join doctors on admissions.attending_doctor_id = doctors.doctor_id group by doctor_id;
-- select patient_id, attending_doctor_id, diagnosis from admissions where (((patient_id % 2 != 0) and (attending_doctor_id in (1,5,19)) ) or ( LEN(CAST(patient_id AS CHAR)) = 3 AND CAST(attending_doctor_id AS CHAR) LIKE '%2%'));
-- select * from admissions where patient_id = 542 order by admission_date desc limit 1;
-- select day(admission_date), count(*) as total_admissions from admissions group by day(admission_date) order by total_admissions desc;
-- select max(weight) - min ( weight) as weight_delta from patients where last_name = 'Maroni';
-- select province_id, sum(height) from patients group by province_id having sum(height) > 7000;
-- select concat(upper(last_name), ',', lower(first_name)) from patients order by first_name desc
-- SELECT first_name, last_name, birth_date FROM patients WHERE year(birth_date) between 1970 AND 1979 order by birth_date;
-- select allergies, count(allergies) as total_diagnosis from patients group by allergies having allergies is not null order by total_diagnosis DESC;
-- select first_name, last_name, 'Patient' as role from patients union all select first_name, last_name, 'Doctor' as role from doctors;
-- select city, count(city) as num_patients from patients group by city order by num_patients DESC, city;
-- 30
-- select patient_id, diagnosis from admissions group by patient_id, diagnosis having count(patient_id) > 1;
-- select first_name, last_name, allergies from patients where allergies in ('Penicillin', 'Morphine') order by allergies, first_name, last_name;
-- select (select count(*) from patients where gender = 'M') as male_count, (select count(*) from patients where gender = 'F') as female_count;
-- select first_name from patients order by len(first_name), first_name;
-- select patients.patient_id, first_name, last_name from patients join admissions on patients.patient_id = admissions.patient_id where admissions.diagnosis = 'Dementia';
-- select patient_id, first_name from patients where first_name LIKE 's%s' and len(first_name) > 5;
-- select first_name from patients group by first_name having count(first_name) = 1;