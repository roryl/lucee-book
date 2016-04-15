# Example Database

All of the SQL and ORM Examples in this book use the [MySQL test database](https://github.com/datacharmer/test_db)


#Installing the Database
Make sure that you have MySQL installed.

##Download and Load the test database

>This needs to be done as the root MySQL user

```
wget https://github.com/datacharmer/test_db/archive/master.zip
yum install unzip
cd test_db-master/
mysql -u root -p < employees.sql
```

##Alter the tables to InnoDB
We are doing this separately so that we do not have to change your MySQL config to InnoDB, if it was configured as MyISAM. 

You can sheck if your tables are alraedy InnoDB by running from MySQL:

`USE employees; SHOW TABLE STATUS;`

```
ALTER TABLE dept_emp ENGINE=InnoDB;
ALTER TABLE dept_manager ENGINE=InnoDB;
ALTER TABLE titles ENGINE=InnoDB;
ALTER TABLE salaries ENGINE=InnoDB;
ALTER TABLE employees ENGINE=InnoDB;
ALTER TABLE departments ENGINE=InnoDB;
```

##Creating a User
We'll use this user to connect form our application. We set localhost and a wildcard host, '%', to cover scenarios where Lucee is installed on the same server as the test database, or a remote server.
```
create database employees;
create user employees@'%' identified by '123456';
grant all on employees.* to employees@'%' identified by '123456';
grant all on employees.* to employees@'localhost' identified by '123456';
flush privileges;
```