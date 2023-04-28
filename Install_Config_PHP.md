# Week 7: Installing and Configuring PHP

---

## Task

1. Install PHP and relevant Apache2 modules

2. Configure PHP and relevant modules to work with Apache2

3. Configure PHP and relevant modules to work with MySQL

Learn how to set up a LAMP (Linux, Apache, MySQL, PHP) stack.

This stack enables us to create a web server that provides extra funtionality via PHP and MySQL, both of which are required to run content management systems and integrated library systems.


### Install PHP

1. **sudo apt install php libapache2-mod-php**

2. **sudo systemctl restart apache2**

3. Check system status: **systemctl status apache2**


### Check Install

1. **cd /var/www/html/**

2. **sudo nano info.php**

3. Add this text to the **info.php** file

<?php
phpinfo();
?>

4. Visit that file using the **external IP** address

- **http://34.70.197.240/info.php**

5. A page that provides system information about PHP, Apache2, and the server should apperar



### Basic Configurations

1. To provide for PHP, we want Apache2 to default to a file titled **index.php** instead of **index.html** file

2. **cd /etc/apache2/mods-enabled/**

3. **sudo cp dir.conf dir.conf.bak**

4. **sudo nano dir.conf**

5. **sudo nano info.php**

6. Change the order to list the **index.php** file before index.html

7. Check configuration: **apachectl configtest**

8. If **Syntax OK**, reload and restart Apache2

- **sudo systemctl reload apache2**

- **sudo systemctl restart apache2**


### Create an index.php File

- **cd /var/www/html/**

- **sudo nano index.php**

- Add the code from <https://cseanburns.github.io/systems-librarianship/15-installing-configuring-php.html>

- open the site again **34.70.197.240**

4. Visit that file using the **external IP** address

- **http://34.70.197.240/**
