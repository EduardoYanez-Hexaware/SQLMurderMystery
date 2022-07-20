SQL
SELECT *
SELECT column_name

FROM table_name

WHERE specific_criteria

E.g.1 SELECT * FROM person WHERE name = 'Kinsey Erickson'

AND another_specific_criteria
OR another_specific_criteria

E.g.2 SELECT * FROM crime_scene_report WHERE type = 'theft' AND city = 'Chicago';

% wildcard
E.g.3 'Ca%a' matches Canada and California

_ wildcard
E.g.4 'B_b' would match 'Bob' and 'Bub' but not 'Babe' or 'Bb'

E.g.5 SELECT DISTINCT city FROM crime_scene_report WHERE city LIKE 'I%';

E.g.6 SELECT DISTINCT city FROM crime_scene_report WHERE city BETWEEN 'W%' AND 'Z%';

E.g.7 SELECT DISTINCT city FROM crime_scene_report WHERE LOWER(city) ='sql city';

Functions:
MAX:    finds the maximum value 
MIN:    finds the minimum value 
SUM:    calculates the sum of the specified column values 
AVG:    calculates the average of the specified column values 
COUNT :    counts the number of specified column values 

ORDER BY query ASC
ORDER BY query DESC