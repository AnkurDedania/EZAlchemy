EZAlchemy
=========

Quickly interact with your database by loading tables to the class EZAlchemy 
which also comes with some helpfull methods for inserting and deleting rows 
a safe way.

Installing:

    $ pip install ezalchemy

Usage:

```python
from ezalchemy import EZAlchemy

DB = EZAlchemy(
    db_user='username',
    db_password='pezzword',
    db_hostname='127.0.0.1',
    db_database='mydatabase',
    d_n_d='mysql'   # stands for dialect+driver
)

# let's suppose we have a table in the database named Cars

# this function loads all tables in the database to the class instance DB
DB.connectAutoload()

# or just load tables that you need to use
DB.connect(['Cars'])

# insert elements a safe way
car = DB.insert(DB.Cars, brand='Audi', year='2009', color='green')
print(car.color)

# query all Cars
all_cars = DB.session.query(DB.Cars).all()

# query certain columns
result = DB.session.query(DB.Cars).filter(DB.Cars.color=='green')
print([r.brand for r in result) 

# delete some elements
result = DB.session.query(DB.Cars).filter(DB.Cars.year < 1980)
DB.delete(result)   # will delete all rows of Cars older than 1980

# We can also use the "engine" to do raw SQL queries
rows = DB.engine.execute('SELECT * from Cards')
for row in rows:
    print row[0], row[1]
```
