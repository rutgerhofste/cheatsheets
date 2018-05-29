# PostgreSQL cheat sheet

Table size:

`SELECT pg_size_pretty(pg_total_relation_size('"<schema>"."<table_name>"'));`


CREATE TABLE test01 (
    name        varchar(40),
    age         integer,
    salary      double precision,
    date_prod   date,
    category    varchar(40)      
);

INSERT INTO test01 (name,age,salary,date_prod,category)
VALUES ('foo', 42 , 10.1 , '2018-12-01','member'),
('bar',43 , 15 , '2018-12-01','member'),
('barz',3 , 40.6 , '2018-12-01','other'),
('fooz',16 , 80.7 , '2018-12-01','other')


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