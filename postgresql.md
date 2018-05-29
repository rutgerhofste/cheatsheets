# PostgreSQL cheat sheet

Table size:

`SELECT pg_size_pretty(pg_total_relation_size('"<schema>"."<table_name>"'));`