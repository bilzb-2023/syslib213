# Week 11: Install WordPress

---

## Task

1. Download and install WordPress.
2. Create a site.
3. Add content.
4. Learn to use WordPress.


---


###Installation

- Read but don't follow the installation instructions. [How to Install WordPress](https://wordpress.org/documentation/article/how-to-install-wordpress/)


###Customized Installation Process###

####Step 1: Requirements####

1. Check the system requirements for WordPress. Run **php --version** and **mysql --version**

2. Add PHP modules

**sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl**

3. Restart Apache2 and MySQL

sudo systemctl restart apache2
sudo systemctl restart mysql


####Step 2: Download and Extract####

1. Change to the /var/www/html directory.

2. Download the latest version of WordPress using the wget program.

3. Extract the package using the tar program.

**cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzvf latest.tar.gz**

As noted in the WordPress documentation, this will create a directory called wordpress in the same directory. Therefore the full path of your installation will located at /var/www/html/wordpress


####Step 3: Create the Database and a User####

1. Switch to the root Linux user

2. Login as the MySQL root user

3. Specifically, we do the following on the command line:

**sudo su
mysql -u root**

The mysql -u root command places us in the MySQL command prompt. The next general instructions are to:

4. Create a new user for the WordPress database

5. Be sure to replace the Xs with a strong password

6. Create a new database for WordPress

7. Grant all privileges to the new user for the new database

8. Examine the output

9. Exit the MySQL prompt

10. The command for numbers 4-9 would look like this:

create user 'wordpress'@'localhost' identified by 'XXXXXXXXX';
create database wordpress;
grant all privileges on wordpress.* to 'wordpress'@'localhost';
show databases;
\q

11. **wordpress.* ** above means that it includes all tables


####Step 4: Setup wp-config.php####

1. Change to the **wordpress** directory

2. Copy and rename the **wp-config-sample.php** file to **wp-config.php**

3. Edit the file and add the WordPress database name, user name, and password in the fields for DB_NAME, DB_USER, and DB_PASSWORD.

4. This means that we specifically do the following:

**cd /var/www/html/wordpress
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php**

5. In nano, add the database name, user, and password in the appropriate fields, just like we did with our login.php file for our bare bones OPAC.

6. Disable FTP uploads to the site. Navigate to the end of the file and add the following line:

**define('FS_METHOD','direct');**


####Step 5: Optional renaming####

1. Setup **wp-config.php**

The WordPress files were installed at /var/www/html/wordpress. This means that your site would be located at:

http://34.70.197.240/wordpress

2. Rename wordpress to blog. I chose to rename mine **library**

**cd /var/www/html**
**sudo mv wordpress library**


####Step 6: Change File Ownership####

1. Use this command   **sudo chown -R www-data:www-data * **


sudo chown -R www-data:www-data *


####Step 7: Run the Install Script####

1. Visit the url  **http://34.70.197.240/library/wp-admin/install.php**

2. **Make sure the directory corresponds to what it is named. I renamed it --library--**

