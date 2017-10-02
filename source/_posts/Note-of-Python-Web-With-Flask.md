---
title: Note of Python Web With Flask
date: 2017-09-30 19:47:04
tags: Python
categories: Python
---

> Put notes of python web here

<!--more-->

1. Install package installation of python
```
> apt-get install python-pip
```
2. Install virtual environment package
```
> pip install virtualenv
```
3. Define an virutal environment. The virtual environment package is installed under **/usr/local/bin/**
```
 > virutalenv <py3env>
 > source <py3env>/bin/activate
 (py3env)>
 (py3env)>deactivate
```
4. Install python3 for the specific virtual environment
```
  virutalenv -p python3 py3env
```
5. Install MySql on ubuntu 16.04
```
> sudo apt-get install mysql-server libmysqlclient-dev -yq
> sudo /etc/init.d/mysql start
```  
6. Intall MySQLdb which is an interface to Python using following command
```
> sudo pip install mysql-python
```
7. Create a user for a specific database
```
> sudo mysql -u root -p
> Enter Password: 
mysql>create database r;
mysql>create user 'web'@'localhost' identified by 'web'
mysql>use r;
Database Changed
mysql>grant all on r.* TO 'web'@'localhost'
mysql>quit;
Bye
```
8. A common operation on MYSQL:
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
