# SQL Cheat Sheet

> NB!
> - dates need to be in quotes! '2015-09-01'


## WHERE statements

Negative condition
```sql
WHERE <column> != <value>
```

searching with a set of values
WHERE <column> IN (<value1>, <value2>, <value3>)
WHERE <column> NOT IN (<value1>, <value2>, <value3>)

searching in a range
(rather than using ">= <value1> AND <= <value2>")
WHERE <column> BETWEEN <minimum> AND <maximum>
WHERE <column> NOT BETWEEN <minimum> AND <maximum>

searching for a pattern
(unlike =, it's case insensitive)
WHERE title LIKE "Harry Potter%Fire"
WHERE title NOT LIKE "Harry Potter%Fire"

searching for empty values
WHERE <column> IS NULL
WHERE <column> IS NOT NULL


## Modifying data

insert values in the order of the columns prescribed in the schema
INSERT INTO <table> VALUES (<value 1>, <value 2>)

insert values (flexible column/value order)
INSERT INTO <table> (<column 1>, <column 2>) VALUES (<value 1>, <value 2>)
- NB: specifying the columns like this allows us to leave out the values for columns that are nullable (by dropping them from both the list of columns and the list of values)

insert multiple rows
INSERT INTO <table> (<column 1>, <column 2>, ...) 
             VALUES 
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...)

update statement
UPDATE <table> SET <column 1> = <value 1>, <column 2> = <value 2>

