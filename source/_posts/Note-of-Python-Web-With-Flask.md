---
title: Note of Python Web With Flask
date: 2017-09-30 19:47:04
tags: Python
categories: Python
---

> Put notes of python web here

<!--more-->

### Install package installation of python ###

```
> apt-get install python-pip

```
### Install virtual environment package ###
```bash
pip install virtualenv 
```

### Define an virutal environment ### 
> The virtual environment package is installed under **/usr/local/bin/**  
```bash
virutalenv <py3env>
source <py3env>/bin/activate
 (py3env)>
 (py3env)>deactivate  
```  

### Install python3 for the specific virtual environment ###

```bash
  virutalenv -p python3 py3env
```

### Install MySql on ubuntu 16.04 ###
```bash
sudo apt-get install mysql-server libmysqlclient-dev -yq
sudo /etc/init.d/mysql start
```

### Intall MySQLdb which is an interface to Python using following command ###

```
sudo pip install mysql-python
```

### Create a user for a specific database ###
```
sudo mysql -u root -p
Enter Password: 
mysql>create database r;
mysql>create user 'web'@'localhost' identified by 'web'
mysql>use r;
Database Changed
mysql>grant all on r.* TO 'web'@'localhost'
mysql>quit;
Bye
```

### A common operation on MYSQL: ###

```
HOSTNAME='localhost'
DATABASE='r'
USERNAME='web'
PASSWORD='web'
DB_URI='mysql://{}:{}@{}/{}'.format(USERNAME, PASSWORD, HOSTNAME, DATABASE)

def Test():
    import MySQLdb

    try:
        con = MySQLdb.connect(HOSTNAME,USERNAME,PASSWORD,DATABASE)
        cur = con.cursor()
        cur.execute("SELECT VERSION()")
        ver = cur.fetchone()
        print("Database version: %s" %ver)
    except MySQLdb.Error as e:
        print("Error %d: %s" %(e.args[0], e.args[1]))
        exit(1)
    finally:
        if con:
            con.close()


if __name__ == "__main__":
    Test()

Output like:
Database version: 5.7.19-0ubuntu0.16.04.1
```

### A sample for RCUD(read,create,update, delete) ###

```
HOSTNAME='localhost'
DATABASE='r'
USERNAME='web'
PASSWORD='web'
DB_URI='mysql://{}:{}@{}/{}'.format(USERNAME, PASSWORD, HOSTNAME, DATABASE)

def TestCRUD():
    import MySQLdb
    con = MySQLdb.connect(HOSTNAME, USERNAME, PASSWORD, DATABASE)

    try:
        with con as cur:
            cur.execute('drop table if exists users')
            cur.execute('create table users(Id INT PRIMARY KEY AUTO_INCREMENT, Name VARCHAR(25))')
            cur.execute("INSERT INTO users(Name) values('rainy1')")
            cur.execute("INSERT INTO users(Name) values('rainy2')")
            cur.execute('SELECT * FROM users')

            rows = cur.fetchall()
            for row in rows:
                print(row)


            print('Before update ...')

            # use %s for all, a tuple for arguments 
            cur.execute('update users set Name=%s where Id=%s', ('rainy', 1))

            print('Update is over')
            cur = con.cursor(MySQLdb.cursors.DictCursor)
            cur.execute('select * from users')

            print("Results after update...")
            rows = cur.fetchall()
            for row in rows:
                #print(row)
                print(row['Id'], row['Name'])

        con.commit()
    except MySQLdb.Error as e:
        con.rollback()
```

###  A sample for SQLAlchemy. When using SQLAlchemy, results can be retrieved from the execution result. ###

```
def TestSQLAlchemy():
    from sqlalchemy import create_engine
    connectionStr = 'mysql+mysqldb://{}:{}@{}/{}'
    engine = create_engine(connectionStr.format(USERNAME, PASSWORD, HOSTNAME, DATABASE))

    with engine.connect() as con:
        rs = con.execute('SELECT * FROM users')
        print(rs.fetchone())
```

### Display line number in** VIM** ###

```
:set nu
```

### ORM on SQLAlchemy example, query filter: ###

```
from sqlalchemy import create_engine, Column, Integer, String, Sequence, text
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import and_, or_

from sqlalchemy.orm import sessionmaker

from consts import DB_URI

print('DB_URI', DB_URI)

eng = create_engine(DB_URI)
Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, Sequence('user_id_seq'), primary_key = True, autoincrement = True)
    name = Column(String(50))

Base.metadata.drop_all(bind = eng)
Base.metadata.create_all(bind = eng)

Session = sessionmaker(bind = eng)

session = Session()

session.add_all([User(name=username) for username in ('rainy1', 'rainy2', 'rainy3')])

session.commit()

def get_result(rs):

    print '-' * 20
    for user in rs:
        print(user.name)


rs = session.query(User).all()
get_result(rs)
rs = session.query(User).filter(User.id.in_([2,]))
get_result(rs)
rs = session.query(User).filter(and_(User.id > 2, User.id < 4))
get_result(rs)
rs = session.query(User).filter(or_(User.id == 2, User.id == 4))
get_result(rs)
rs = session.query(User).filter(User.name.like('%ai%'))
get_result(rs)
user = session.query(User).filter_by(name='rainy1').first()
get_result([user])

	ession.query(User).filter(text('id > 2 and id < 4')).order_by(text('id')).all()
get_result(rs)
rs = session.query(User).filter(text('id<:value and name=:name')).params(value = 3, name='rainy2').all()
get_result(rs)
rs = session.query(User).from_statement(text('SELECT * FROM users where name=:name')).params(name='rainy1').all()
get_result(rs)
```

### A SQLAlchemy sample with foregin key reference ###
```bash
from sqlalchemy import create_engine, Column, Integer, String, ForeignKey
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker, relationship

from consts import DB_URI

eng = create_engine(DB_URI)
Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True, autoincrement=True)
    name = Column(String(50))


class Address(Base):
    __tablename__ = 'addresss'

    id = Column(Integer, primary_key=True, autoincrement=True)
    email_address = Column(String(128), nullable=False)
    user_id = Column(Integer, ForeignKey('users.id'))
    user = relationship('User', back_populates='addresses')


User.addresses = relationship('Address', order_by=Address.id, back_populates='user')
Base.metadata.drop_all(bind=eng)
Base.metadata.create_all(bind=eng)

Session = sessionmaker(bind=eng)
session = Session()

user = User(name='rainy')
user.addresses = [Address(email_address='a@test.com', user_id=user.id),
                  Address(email_address='b@test.com', user_id=user.id)]

session.add(user)
session.commit()

for u, a in session.query(User, Address).filter(User.id == Address.user_id).\
filter(Address.email_address == 'a@test.com').all():
    print('User ID:{}'.format(u.id))
    print('Email Address:{}'.format(a.email_address))

```

### Install Flask-SQLAlchemy ###
```
pip install Flask-SQLAlchemy
```

### A sample for using Flask-SQLAlchemy ### 

> const.py
```
HOSTNAME = 'localhost'
DATABASE = 'r'
USERNAME = 'web'
PASSWORD = 'web'
DB_URI = 'mysql://{}:{}@{}/{}'.format(USERNAME, PASSWORD, HOSTNAME, DATABASE)
```

> config.py
```
from consts import DB_URI

DEBUG = True

SQLALCHEMY_DATABASE_URI = DB_URI

SQLALCHEMY_TRACK_MODIFICATIONS = False

```
> ext.py
```
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()
~                    
```
> user.py
```
from ext import db

class User(db.Model):
    __tablename__ = 'users'

    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    name = db.Column(db.String(50))

    def __init__(self, name):
        self.name = name
```
> app.py
```
from flask import Flask, request, jsonify
from ext import db
from users import User

app = Flask(__name__)

app.config.from_object('config')

db.init_app(app)

with app.app_context():
    db.drop_all()
    db.create_all()


@app.route('/users/', methods=['POST'])
def users():
    username = request.form.get('name')
    user = User(username)
    print('User ID:{}'.format(user.id))
    db.session.add(user)
    db.session.commit()

    return jsonify({'id': user.id})

if __name__=='__main__':
    app.run(host='0.0.0.0', port=9000)
```

### Make a post request to test ###
> Make a post request to test the above app
```
import json, urllib2
from consts import RequestURI

textmod={"username":"rainy"}
textmod=json.dumps(textmod)
#print(textmod)

header_dict={'User-Agent':'Mozilla/5.0 (Windows NT 6.1; Trident/7.0; rv:11.0) like Gecko', "Content-Type": "application/json"}
url=RequestURI
req = urllib2.Request(url=url, data=textmod, headers=header_dict)
res = urllib2.urlopen(req)
res = res.read()
print(res)
```
