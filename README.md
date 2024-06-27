# Psycopg3, Psyco2 and SQLAlchemy2.x versions practice

## Psycopg3
### Psycopg3 New Connection Object

### Psycopg3 Multiple Inserts

Multiple inserts in psycopg are done using Pipeline mode usage. The main command is `cursor.executemany`.
Psycopg supports the pipeline mode via the Connection.pipeline() method. The method is a context manager: entering the with block yields a Pipeline object. At the end of block, the connection resumes the normal operation mode.

Within the pipeline block, you can use normally one or more cursors to execute several operations, using `Connection.execute()`, `Cursor.execute()` and `executemany()`.

```python
with conn.pipeline():
    conn.execute("INSERT INTO mytable VALUES (%s)", ["hello"])
    with conn.cursor() as cur:
        cur.execute("INSERT INTO othertable VALUES (%s)", ["world"])
        cur.executemany(
            "INSERT INTO elsewhere VALUES (%s)",
            [("one",), ("two",), ("four",)])

```

