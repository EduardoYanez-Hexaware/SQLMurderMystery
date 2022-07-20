You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.

TABLES
crime_scene_report
drivers_license
person
facebook_event_checkin
interview
get_fit_now_member
get_fit_now_check_in
income
solution

CREATE TABLE crime_scene_report ( date integer, type text, description text, city text )

<!-- First query -->
SELECT * from crime_scene_report
WHERE date = '20180115'
AND city = 'SQL City'
AND type = 'murder';

<!-- Result first query
  date: 20180115
  type: murder
  description: Security footage shows that there were 2 witnesses. The first witness lives at the last house on "Northwestern Dr". The second witness, named Annabel, lives somewhere on "Franklin Ave".
  city: SQL City
>

<!-- First witness -->
SELECT * from person
WHERE address_street_name = 'Northwestern Dr'
ORDER BY address_number DESC; <!-- Morty Schapiro>

SELECT * FROM person
WHERE address_street_name = 'Northwestern Dr'
AND id = '14887'
AND name = 'Morty Schapiro'
AND license_id = '118009'
AND address_number = '4919'
AND ssn = '111564949';

<!-- Second witness
  The second witness, named Annabel, lives somewhere on "Franklin Ave".
-->
SELECT * FROM person
WHERE address_street_name = 'Franklin Ave'
AND name LIKE 'Annabel%';

<!-- Result second witness 
  id: 16371
  name: Annabel Miller
  license_id: 490173
  address_number: 103
  address_street_name: Franklin Ave
  ssn: 318771143
-->

<!-- Interview transcripts -->
SELECT * FROM interview
WHERE person_id = '14887'
OR person_id = '16371'; <!-- this wont show names, just basic info-->

SELECT person.name, interview.transcript
FROM interview JOIN person
ON person.id = interview.person_id
WHERE person.id = '14887' OR person.id = '16371'; <!-- this shows all needed info -->

<!--
Morty Schapiro: I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag. The membership number on the bag started with "48Z". Only gold members have those bags. The man got into a car with a plate that included "H42W".

Annabel Miller: I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th.

-->

<!-- Murder info -->
SELECT * FROM get_fit_now_check_in
WHERE membership_id LIKE '48Z%'
AND check_in_date = '20180109';
<!-- 48Z7A or 48Z55 -->

SELECT * FROM get_fit_now_member
WHERE id = '48Z7A'; <!-- Joe Germuska person_id: 28819 -->
<!-- Interview
Not found
-->

SELECT * FROM get_fit_now_member
WHERE id = '48Z55'; <!-- Jeremy Bowers person_id: 67318 -->
<!-- Interview
I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017. 
-->

SELECT * FROM drivers_license
WHERE plate_number LIKE '%H42W%'
AND gender = 'male';
id	age	height	eye_color	hair_color	gender	plate_number	car_make	car_model
423327	30	70	brown	brown	male	0H42W2	Chevrolet	Spark LS
664760	21	71	black	black	male	4H42WR	Nissan	Altima

<!-- Murder head info -->
SELECT * FROM drivers_license
WHERE LOWER(hair_color) = 'red'
AND LOWER(car_make) = 'tesla'
AND LOWER(car_model) = 'model s'
AND height < 67
AND height > 65;

<!-- 1. license_id: 202298, 2. license_id: 291182
    1.1 id: 99716 / Miranda Priestly, 2.2 id: 90700 / Regina George
I know that she attended the SQL Symphony Concert 3 times in December 2017.
-->

SELECT * FROM facebook_event_checkin
WHERE person_id = '99716';

<!--
  BINGO! Miranda Priestly
person_id	event_id	event_name	date
99716	1143	SQL Symphony Concert	20171206
99716	1143	SQL Symphony Concert	20171212
99716	1143	SQL Symphony Concert	20171229
-->
