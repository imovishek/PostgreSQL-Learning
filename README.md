# Brilliant-Cloud-Research-Project

Suppose these are my two databases.

```
create table person (
	id BIGSERIAL NOT NULL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	email VARCHAR(150),
	gender VARCHAR(7) NOT NULL,
	date_of_birth DATE NOT NULL,
	country_of_birth VARCHAR(50)
);

create table car (
	id BIGSERIAL NOT NULL PRIMARY KEY,
	make VARCHAR(50) NOT NULL,
	model VARCHAR(50) NOT NULL,
	price VARCHAR(150)
);
```

## Import sql commands from file
\i file_name

#To alter view
\x

## Now() returns the current time stamps
```
SELECT (NOW() + INTERVAL '10 MONTHS')::DATE; 
=> 2021-02-10 'YYYY MM DD
```
## Extract year or month or day
```
SELECT EXTRACT(YEAR FROM NOW()); 
=> 2020
```
## Age Function
```
SELECT first_name, last_name, AGE(NOW(), date_of_birth) AS age;
```
## Dropping constraint like primary key
```
ALTER TABLE person DROP CONSTRAINT person_pkey;
```

## Adding primary key constraint
```
ALTER TABLE person ADD PRIMARY KEY (id);
```

## Delete records from table
```
DELETE FROM person WHERE id = 1;
```

## Making column unique
```
ALTER TABLE person ADD CONSTRAINT unique_email_address UINQUE(email)
```

## Adding constriaint like schema rules
```
ALTER TABLE person ADD CONSTRAINT gender_constraint CHECK(gender = 'Female' OR gender = 'Male');
```

## Delete records
```
DELETE FROM person WHERE id = 1011;
```

## Update records
```
UPDATE person SET email = 'omar@gmail.com', first_name = 'Omar' WHERE id = 2011;
```

## Error Handling on conflict command
'it is an insert command with duplicate id ( make sure id is unique )
```
INSERT INTO (id,,,) VALUES (15,,,) ON CONFLICT (id) DO NOTHING
```

## Upsert, UPDATE after Error found!
' email is from db but EXLUDE.email from values
```
INSERT INTO (id,,,) VALUES (15,,,) ON CONFLICT (id) DO UPDATE SET email = EXCLUDE.email;
```

## Forein key

' in person table car_id is a forein key which reference to car table
```
car_id BIGINT REFERENCES car(id), UNIQUE (car_id) 
```

' in car table and it's id is primary key
```
id BIGINT NOT NULL PRIMARY KEY 
```

## Join to tables
```
SELECT * FROM person JOIN car ON person.car_id = car.id; 
```
' one can use person.first_name, car.make, car.model instead of *

## Left Join
```
SELECT * FROM person LEFT JOIN car ON person.car_id = car.id; 
```
' it just populates all records of left table even they have no relationship
 
#CASCADE deletes all the forein key referring rows also (need to learn)

## Exporting QUERY resutls to csv
```
\copy (SELECT * FROM person LEFT JOIN car ON person.car_id = car.id) TO '/home/ovishek/Desktop/result.csv' DELIMITER ',' CSV HEADER;
```
## Update auto increment value for BIGSERIAL
```
ALTER SEQUENCE person_id_seq RESTART WITH 10;
```
## To add an Extension

' you need super user access for that
' for getting super user access run these commands
```
\q ' exit from psql 
sudo -u postgres psql postgres 'entering super user 
ALTER USER mydb_user WITH SUPERUSER; 'getting super user access to user 
\q ' exit from psql 
psql mydb_user 
 
SELECT * FROM pg_available_extensions; 
CREATE EXTENSION IF NOT EXISTS "uuid-ossp"; 
```
## HOW to use uuid
' to see functions
```
\df 
SELECT uuid_generate_v4(); 
INSERT INTO (_id,,,,) VALUES (uuid_generate_v4(),,,,) 
```

