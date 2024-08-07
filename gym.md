1.creacion de la oriemra tabla llamda routine.

```
CREATE TABLE routine (
    id SERIAL PRIMARY KEY,
    description TEXT NOT NULL,
    disclaimer TEXT,
    sex CHAR(1) NOT NULL
);```
llenamos los datos de las tablas :
2.creacion de la segunda tabla 

```
CREATE TABLE exercise (
    id SERIAL PRIMARY KEY,
    detail TEXT NOT NULL,
    video_url TEXT
);
```
3.creacion de la tercer tabla agregando las como foreign key a las dos tablas anteriores 

```
CREATE TABLE routine_exercise (
    id SERIAL PRIMARY KEY,
    series INT NOT NULL,
    repetitions INT NOT NULL,
    routine_id INT NOT NULL,
    exercise_id INT NOT NULL,
    FOREIGN KEY (routine_id) REFERENCES routine (id),
    FOREIGN KEY (exercise_id) REFERENCES exercise (id)
);
```
4llenamos los datos de las tablas segun el order expecificado de cat tabla utlizando el inser to ,siempre debemos de tomar en cuenta la escritura y el order que fue creada la tabla ,caso contrario nos dara error:

```
INSERT INTO exercise (detail, video_url) VALUES 
('Push-up', 'https://example.com/pushup'),
('Sit-up', 'https://example.com/situp'),
('Squat', 'https://example.com/squat'),
('Lunges', 'https://example.com/lunges'),
('Plank', 'https://example.com/plank');```
<img src="![./capturas/sentence01.png](<CAPTURAS /Captura de pantalla 2024-08-06 a la(s) 6.47.48 p. m..png>)" alt="drawing" width="500"/>
```
INSERT INTO routine (description, disclaimer, sex) VALUES 
('Morning Routine', 'Consult a doctor before starting', 'M'),
('Evening Routine', 'For experienced athletes', 'F'),
('Full Body Workout', 'Perform each exercise with proper form', 'M'),
('Cardio Blast', 'Stay hydrated', 'F'),
('Strength Training', 'Warm-up before starting', 'M');```
<img src="![./capturas/sentence01.png](<CAPTURAS /Captura de pantalla 2024-08-06 a la(s) 6.47.33 p. m..png>)" alt="drawing" width="500"/>
```
INSERT INTO routine_exercise (series, repetitions, routine_id, exercise_id) VALUES 
(3, 15, 1, 1),  -- Morning Routine includes Push-up
(3, 20, 1, 2),  -- Morning Routine includes Sit-up
(4, 10, 2, 3),  -- Evening Routine includes Squat
(2, 12, 3, 4),  -- Full Body Workout includes Lunges
(3, 30, 4, 5);  -- Cardio Blast includes Plank
```
por ultimo creamos una tabla con una solo vista de las tres donde proporciona una vista completa de las tablas,mostrando informacion mas detallada y asi no nesecitamos estar consultando de manera individual. 
<img src="![./capturas/sentence01.png](<CAPTURAS /Captura de pantalla 2024-08-06 a la(s) 6.46.51 p. m..png>)" alt="drawing" width="500"/>
.
```CREATE VIEW routine_details AS
SELECT
    r.id AS routine_id,
    r.description AS routine_description,
    r.disclaimer AS routine_disclaimer,
    r.sex AS routine_sex,
    re.series AS exercise_series,
    re.repetitions AS exercise_repetitions,
    e.detail AS exercise_detail,
    e.video_url AS exercise_video_url
FROM routine r
JOIN routine_exercise re ON r.id = re.routine_id
JOIN exercise e ON re.exercise_id = e.id;
```



