# PostgreSQL cheat sheet

Table size:

`SELECT pg_size_pretty(pg_total_relation_size('"<schema>"."<table_name>"'));`

DROP TABLE IF EXISTS test01

CREATE TABLE test01 (
    name        varchar(40),
    age         integer,
    salary      double precision,
    date_prod   date,
    category    varchar(40),
    year        integer,
    month       integer      
);

INSERT INTO test01 (name,age,salary,date_prod,category,year,month)
VALUES ('foo', 42 , 10.1 , '2018-12-01','member',1960,1),
('bar',43 , 15 , '2018-12-01','member',1960,2),
('barz',3 , 40.6 , '2018-12-01','other',1970,1),
('fooz',16 , 80.7 , '2018-12-01','other',1970,2)


#  Window functions:

https://compose.com/articles/metrics-maven-window-functions-in-postgresql/

SELECT name AS test_name,  
       age AS test_age,
       category,
       SUM(age)
            OVER(PARTITION BY category) AS category_age
FROM test01 
ORDER BY name  


Window frames in window functions use UNBOUNDED PRECEDING by default, more accurately RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW, when an ORDER BY is specified.

# Add new column

`ALTER TABLE test01 ADD COLUMN bonus double precision DEFAULT 0.0`

# Update value based on other colums

`UPDATE test01
SET bonus = salary + age`

`ALTER TABLE test01 ADD COLUMN date_column DATE`

`UPDATE test01
	SET date_column = '2001-13-28'`

UPDATE test01
    SET date_column = make_date(year, month, 1);


 `ALTER TABLE test01 ADD COLUMN month_from_date integer`

 `UPDATE test01
     SET month_from_date = date_part('month', date_column)`