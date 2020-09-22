# Data-engineering-learning

### Connecting with PostgresSQL
```python
import psycopg2
# Connect to server
conn = psycopg2.connect("dbname=<> user=<>")

```
### Interacting with Database
```python
# Obtain cursor object for this connection
cur = conn.cursor()
# Excute sql query
cur.execute("SELECT * FROM user")

# to get one result
one_result = cur.fetchone()
# to get all results
all_result = cur.fetchall()
```
### Create table
```python
cur.execute("""
CREATE TABLE users(id integer PRIMARY KEY,email text,name text, address text);
""")
```
### Inserting into values
```python
cur.execute("INSERT INTO users VALUES (%s, %s, %s, %s);", (2, 'sherlocksh@mail.in', 'Sherlock', '221B Baker's Street'))
```

### Pushing data from csv into database
`accounts.csv` with fields `id`, `email`, `name`, `address`

```python
import csv
with open('accounts.csv', 'r') as file:
    next(file) # skip csv header (first row with column titles)
    reader = csv.reader(file)
    for row in reader:
        cur.execute("INSERT INTO users VALUES (%s, %s, %s, %s);", row)
        
```

### Commit and close database connection
```python
#committing changes
conn.commit()

# Close connection
conn.close()
```

### Type names 
[docs](https://www.postgresql.org/docs/9.6/catalog-pg-type.html)
```python
cur.execute("SELECT typname FROM pg_catalog.pg_type WHERE oid = 25;")
type_name_25 = cur.fetchone()[0]
print(type_name_25)

cur.execute("SELECT typname FROM pg_catalog.pg_type WHERE oid = 700;")
type_name_700 = cur.fetchone()[0]
print(type_name_700)
```
