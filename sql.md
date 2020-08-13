# MySQL

```bash
#temporary password location
sudo grep 'temporary password' /var/log/mysqld.log

#login
mysql -u root -p${password}
#changes password
ALTER USER 'root'@'localhost' IDENTIFIED BY '${new_password}';


#show databases
SHOW DATABASES;

#create database
CREATE DATABASE ${database_name};

#select a database
USE ${database_name};

#create a table
CREATE TABLE ${table_name}
(
    Name varchar(25),
    Age int,
    Location varchar(255),
    ${field_name} ${datatype}
);

#show tables
SHOW TABLES;

#insert data in table
INSERT INTO persons values ("John Doe", 25, "New York");

#show data of a table
SELECT * FROM persons;

# the root user is the default user that mysql creates root user has all permission by default

#create a user
CREATE USER 'john'@'localhost' IDENTIFIED BY 'MyNewPassword';
            'username'@'host'                'password'
#create a user to specific host
CREATE USER 'john'@'192.168.1.10' IDENTIFIED BY 'MyNewPassword';

#if you want a new user to connect in all system
CREATE USER 'john'@'%' IDENTIFIED BY 'MyNewPassword';

#grant user privileges
GRANT ${permission} ON ${db.table} TO 'username@localhost';

#grant select to school db but only persons table
GRANT SELECT ON school.persons TO 'username@localhost';

#grant select and update to school db but only persons table
GRANT SELECT, UPDATE ON school.persons TO 'username@localhost';
#grant select and update to db school on any table
GRANT SELECT, UPDATE ON school.* TO 'username';
#grant all privileges to any db or table
GRANT ALL PRIVILEGES ON *.* TO 'username@localhost';
#show grants for all user
SHOW GRANTS FOR 'username@localhost';

# list of privileges
|---------------------|-----------------------------|
|PRIVILEGES           | DESCRIPTION                 |
|---------------------|----------------------- -----|
|ALL PRIVILEGES       |Grant all access             |
|CREATE               |Create databases             |
|DROP                 |delete databases             |
|DELETE               |delete rows from table       |
|INSERT               |insert rows from table       |
|SELECT               |Read/Query from table        |
|UPDATE               |Update rows from table       |
|---------------------------------------------------|
```

# MongoDB
_______________________Collection_____________________________________|
|  |-----------------------------||-----------------------------|    |
|  |{                            ||{                            |    |
|  |    "name": "John",          ||    "name": "John",          |    |
|  |    "age": 12,               ||    "age": 12,               |    |
|  |    "location": "New York"   ||    "location": "New York"   |    |
|  |}                            ||}                            |    |
|  |--------Document-------------||--------Document-------------|    |
|____________________________________________________________________|

```bash
#to start mongodb
sudo service mongod start

#logs location
cat /var/log/mongodb/mongod.log

#mongodb config file location
/etc/mongod.conf

#connect to the mongo shell
mongo

#show list of databases
show dbs

#to create or use a database
use ${database_name} # use school

#to know which database that you are currently using
db

#to create a collection
db.create("${collection_name}")

#to show collections
show collections

#add new document to a collection
db.persons.insert({
    "name": "John Doe",
    "age": 45,
    "location": "New York"
})

#retrieve datas to collection
db.persons.find()

#search to a collection
db.persons.find({"name": "John Doe"})

```