# Week 7-3: Installing and Configuring MySQL

---

## Task

1. Install PHP and relevant Apache2 modules

2. Configure PHP and relevant modules to work with Apache2

3. Configure PHP and relevant modules to work with MySQL

Learn how to set up a LAMP (Linux, Apache, MySQL, PHP) stack.

This stack enables us to create a web server that provides extra funtionality via PHP and MySQL, both of which are required to run content management systems and integrated library systems.


### Install and Set Up MySQLInstall PHP

1. **sudo apt install mysql-server**

2. **systemctl status mysql 
**

3. Become the **root Linux user**.

- **sudo su**

4. Connect to the MySQL server as the MySQL root user

- **mysql -u root**

5. Request a list of the databases

- **show databases;**

+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.002 sec)



### Create and Set Up a Regular User Account

1. **create user 'opacuser'@'localhost' identified by 'XXXXXXXXX';**


### Create a Practice Database

- create database opacdb;
- grant all privileges on opacdb.* to 'opacuser'@'localhost';
- show databases;

- **\q** to exit back to the normal Linux user account

- **exit** to exit out of the Linux root user account


### Logging in as Regular User and Creating Tables

- mysql -u opacuser -p

- show databases;

- use opacdb;

- create table books (
id int unsigned not null auto_increment,
author varchar(150) not null,
title varchar(150) not null,
copyright date not null,
primary key (id)
);

- show tables;
describe books;


### Adding records into the table

- insert into books (author, title, copyright) values
('Jennifer Egan', 'The Candy House', '2022-04-05'),
('Imbolo Mbue', 'How Beautiful We Were', '2021-03-09'),
('Lydia Millet', 'A Children\'s Bible', '2020-05-12'),
('Julia Phillips', 'Disappearing Earth', '2019-05-14');

- view all records just created: **select * from books;**


### Testing Commands

**Reminder: each MySQL command ends with a semi-colon. Some of the following MySQL commands are single-line, but others are multi-line. Regardless if a MySQL command is one-line or multi-line, it doesn't end until it ends with a semi-colon**

select author from books;
select copyright from books;
select author, title from books;
select author from books where author like '%millet%';
select title from books where author like '%mbue%';
select author, title from books where title not like '%e';
select * from books;
alter table books add publisher varchar(75) after title;
describe books;
update books set publisher='Simon \& Schuster' where id='1';
update books set publisher='Penguin Random House' where id='2';
update books set publisher='W. W. Norton \& Company' where id='3';
update books set publisher='Knopf' where id='4';
select * from books;
delete from books where author='Julia Phillips';
insert into books
(author, title, publisher, copyright) values
('Emma Donoghue', 'Room', 'Little, Brown \& Company', '2010-08-06'),
('Zadie Smith', 'White Teeth', 'Hamish Hamilton', '2000-01-27');
select * from books;
select author, publisher from books where copyright < '2011-01-01';
select author from books order by copyright;
\q


### Install PHP and MySQL Support

1. sudo apt install php-mysql php-mysqli

2. sudo systemctl restart apache2

3. sudo systemctl restart mysql


### Create PHP Scripts

- cd /var/www/html/
sudo touch login.php
sudo chmod 640 login.php
sudo chown :www-data login.php
ls -l login.php
sudo nano login.php

- <?php // login.php
$db_hostname = "localhost";
$db_database = "opacdb";
$db_username = "opacuser";
$db_password = "XXXXXXXXX";
?>

- sudo nano opac.php

- Add the text from [Dr. Burns' Systems Librarianship Book](https://cseanburns.github.io/systems-librarianship/16-installing-configuring-mysql.html)

- Test Syntax

- sudo php -f login.php

- sudo php -f index.php
