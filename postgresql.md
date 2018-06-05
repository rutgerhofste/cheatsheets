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


INSERT INTO test01 (name,age,salary,date_prod,category,year,month)
VALUES ('foo', 42 , 10.1 , '2018-12-01','member',1960,1),
('bar',43 , 15 , '2018-12-01','member',1960,2),
('bar',43 , 15 , '2018-12-01','member',1960,3),
('bar',43 , 15 , '2018-12-01','member',1960,4),
('barz',3 , 40.6 , '2018-12-01','other',1961,1),
('barz',3 , 40.6 , '2018-12-01','other',1961,2),
('barz',3 , 40.6 , '2018-12-01','other',1961,3),
('barz',3 , 40.6 , '2018-12-01','other',1961,4),
('barz',3 , 40.6 , '2018-12-01','other',1962,1),
('barz',3 , 40.6 , '2018-12-01','other',1962,2),
('barz',3 , 40.6 , '2018-12-01','other',1962,3),
('barz',3 , 40.6 , '2018-12-01','other',1962,4),
('fooz',16 , 80.7 , '2018-12-01','other',1970,1),
('fooz',16 , 80.7 , '2018-12-01','other',1970,2),
('fooz',16 , 80.7 , '2018-12-01','other',1970,3),
('fooz',16 , 80.7 , '2018-12-01','other',1970,4)


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


## Moving Average test

CREATE TABLE ma_test (
    pfaf_id     integer,
    year        integer,
    month       integer,
    ptotww      double precision    
);

INSERT INTO ma_test (pfaf_id, year, month, ptotww)
VALUES 
(100000, 1960, 1, 1.0),
(100000, 1961, 1, 2.0),
(100000, 1962, 1, 3.0),
(100000, 1963, 1, 4.0),
(100000, 1964, 1, 5.0),
(100000, 1965, 1, 6.0),
(100000, 1966, 1, 7.0),
(100000, 1967, 1, 8.0),
(100000, 1968, null, 9.0),
(100000, 1969, 1, null),
(100000, 1970, 1, 11.0)

`ALTER TABLE ma_test ADD COLUMN date_column DATE`

`ALTER TABLE ma_test ADD COLUMN ma10_ptotww double precision`

`SELECT year, ptotww,
	   SUM(ptotww)
	       OVER(ORDER BY year ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) as sum_ptotww
FROM ma_test`



SELECT year,month, ptotww_m_30spfaf06, temporal_resolution,
    SUM(ptotww_m_30spfaf06)
        OVER(ORDER BY year ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) as ptotwwma_m_30spfaf06 
FROM y2018m05d29_rh_total_demand_postgis_30spfaf06_v01_v01
WHERE temporal_resolution = 'year'
LIMIT 200



http://sqlfiddle.com/#!17/f4746/2

CREATE TABLE test01 (
    value      double precision,
    year        integer,
    month       integer      
);

INSERT INTO test01 (value,year,month)
VALUES (1 , 1960, 1),
(2 , 1960, 2),
(3 , 1960, 3),
(4 , 1961, 1),
(5 , 1961, 2),
(6 , 1961, 3),
(7 , 1962, 1),
(8 , 1962, 2),
(9 , 1962, 3)


SELECT value, year, month,
  SUM(value)
    OVER(PARTITION BY month ORDER BY year ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) as ma2_value
FROM test01

http://sqlfiddle.com/#!17/a73ac/5



