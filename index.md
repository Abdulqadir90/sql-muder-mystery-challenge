https://mystery.knightlab.com/

A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.

interview
get_fit_now_check_in
get_fit_now_member
person
drivers_license
income
solution
facebook_event_checkin
crime_scene_report

<!-- CREATE TABLE crime_scene_report ( date integer, type text, description text, city text )

date	type	description	city -->

SELECT *
FROM crime_scene_report
WHERE date = 20180115 AND city = "SQL City" AND type = "murder"

 2 witnesses.
 The first witness lives at the last house on "Northwestern Dr".
 The second witness, named Annabel, lives somewhere on "Franklin Ave".

 -------------------

SELECT *
FROM person
WHERE address_street_name = "Northwestern Dr"
ORDER BY address_number DESC
LIMIT 1

first witness = 14887	Morty Schapiro	118009	4919	Northwestern Dr	111564949

SELECT *
FROM person
WHERE address_street_name = "Franklin Ave"
AND name LIKE "%Annabel%"

second witness = 16371	Annabel Miller	490173	103	Franklin Ave	318771143
--------------------

SELECT *
FROM person
WHERE id IN (16371,14887)
shows both witnesses in a table

---------------------

SELECT *
FROM interview
WHERE person_id IN (16371,14887)

morty 14887 - I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag. The membership number on the bag started with "48Z". Only gold members have those bags. The man got into a car with a plate that included "H42W".

annabel 16371 - I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th.

------------------------

The membership number on the bag started with "48Z".
he man got into a car with a plate that included "H42W".
I recognized the killer from my gym when I was working out last week on January the 9th.

SELECT *
FROM drivers_license
WHERE plate_number LIKE "%H42W%"

183779	21	65	blue	blonde	female	H42W0X	Toyota	Prius
423327	30	70	brown	brown	male	0H42W2	Chevrolet	Spark LS
664760	21	71	black	black	male	4H42WR	Nissan	Altima

---------------------

SELECT *
FROM drivers_license AS dl
INNER JOIN person AS p ON dl.id = p.license_id
INNER JOIN get_fit_now_member AS gf ON p.id = gf.person_id
WHERE plate_number LIKE "%H42W%"

id	age	height	eye_color	hair_color	gender	plate_number	car_make	car_model	id	name	license_id	address_number	address_street_name	ssn	id	person_id	name	membership_start_date	membership_status

423327	30	70	brown	brown	male	0H42W2	Chevrolet	Spark LS	67318	Jeremy Bowers	423327	530	Washington Pl, Apt 3A	871539279	48Z55	67318	Jeremy Bowers	20160101	gold

Jeremy Bowers! you do not have the say anything but it may harm your defence if you do not mention when questioned something which you later rely on in court!!!!

