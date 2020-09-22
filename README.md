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
CREATE TABLE users(id integer PRIMARY KEY,
email text,name text, address text);
""")
```

### Commit and close database connection
```python
#committing changes
conn.commit()

# Close connection
conn.close()
```
