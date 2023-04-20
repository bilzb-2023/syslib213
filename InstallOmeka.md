*Week 11:  Install Omeka

---

Omeka is an "Open-source web publishing platforms for sharing digital collections and creating media-rich online exhibits." Most if not all of you have already used Omeka in a prior course. Here our task is not to learn information/knowledge organization, per se, but to learn how to administer the Omeka digital library platform.

---
**The Task

So far we have created our own bare bones OPAC/ILS and we have downloaded, installed, and configured WordPress on our servers. We will use the same basic process to download, install, and configure Omeka.
However, instead of providing comprehensive instructions, your goal is to take what you learned from the bare bones OPAC/ILS and WordPress assignments, and apply them to the Omeka installation and setup. Below are some additional prerequisites that you should complete first. After you've completed them, move on to the General Steps section to remind yourself of the overall process.
You can do it! Be sure to ask and discuss on our chat server.

***System Requirements

All major software has dependencies. For example, our bare bones OPAC depends on MySQL and PHP to provide the database (MySQL) and the glue (PHP) between our HTML and the database. The same is true for Omeka. However, since Omeka is much more complicated software than our bare bones OPAC, its dependencies are stricter. This means that when we plan to download software outside of the apt ecosystem, we need to make sure that our systems meet the requirements for our installation. The Omeka.org Requirements page states that the Omeka Classic installation requires Linux operating system, Apache HTTP server (with mod_rewrite enabled), MySQL version 5.0 or greater, PHP scripting language version 5.6 or higher (with mysqli and exif extensions installed), and, ImageMagick image manipulation software (for resizing images).
We can check that our systems meet these requirements with the following commands:

php --version
mysql --version

Since we completed updating our systems with the OPAC/ILS and WordPress assignments, we can proceed.

---

***Install Prerequisites

--

When we installed WordPress, we installed most of the prerequisites that Omeka needs, but there are a couple of additional things we need to do.

Install ImageMagick: this is a suite of utilities to work with photo files. Omeka uses ImageMagick to create thumbnail images of any photo uploaded to the digital library. See Imagemagick for more information.

From bbilz@syslib-2023:/var/www/html$

sudo apt install imagemagick


Enable Apache mod_rewrite. This is an Apache module used to rewrite URLs. Omeka uses this to create appropriate URLs for items and collections in its digital libraries.

from bbilz@syslib-2023:

sudo a2enmod rewrite

You should be instructed to restart Apache after enabling rewrite:

sudo systemctl restart apache2


Next, we need to add some additional PHP modules to our system to let Omeka operate at full functionality. We can install these using the apt command:
sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl

Then restart Apache2 and MySQL:

sudo systemctl restart apache2

sudo systemctl restart mysql


***General Steps

---

You have already completed all the steps below when you created a bare bones OPAC/ILS and installed WordPress. Your task is to apply what you've learned by completing an Omeka installation on your own. (You can work together and discuss on our chat server.)
Note that the process is very similar to what we have already done with our bare bones OPAC/ILS and our WordPress installations. Use this handbook to remind you of the specific commands. In short, you are going to complete the following steps:


***Download and Extract

---

The next step is to download and extract the Omeka software, which is downloaded as a tar.gz file. This is very much like a compressed zip file. Although we only download one file, when we extract it with the tar command, the extraction will result in a new directory that contains multiple files and subdirectories. The general instructions include:

Change to the /var/www/html directory.

Download the latest version of Omeka using the wget program.

Extract the package using the tar program.

Use wget from your server to download Omeka Classic as a Zip file and extract it in /var/www/html:

https://github.com/omeka/Omeka/releases/download/v3.1/omeka-3.1.zip

unzip it with the unzip command, which you will have to install with the apt command.

the extracted directory will be named omeka-3.1. You might want to rename it simply omeka
Specifically, we do the following on the command line:

from bbilz@syslib-2023:

cd /var/www/html

sudo wget https://github.com/omeka/Omeka/releases/download/v3.1/omeka-3.1.zip/latest.tar.gz

sudo tar -xzvf latest.tar.gz

To rename your omeka-3.1 directory to something else. If you decide to change it, be sure to keep the name lowercase and one word (no spaces and only alphabetic characters). For example:

cd /var/www/html

sudo mv omeka-3.1 omeka

The Omeka files were installed at /var/www/html/omeka. This means that your site would be located at:
http://34.70.197.240/omeka

***Create a new user and a new database

---

Create a new user and a new database in MySQL for the Omeka installation (do not re-use the WordPress database, user, or credentials).

We are going to create the Omeka database and a database user using the same process we used to create a database and user for our bare bones OPAC. The general instructions are:

Switch to the root Linux user

Login as the MySQL root user


Specifically, we do the following on the command line:

From root@syslib-2023:/var/www/html/omeka#

sudo su

mysql -u root

The mysql -u root command places us in the MySQL command prompt. The next general instructions are to:

Create a new user for the Omeka database

Be sure to replace the Xs with a strong password

Create a new database for Omeka

Grant all privileges to the new user for the new database

Examine the output

Exit the MySQL prompt

Specifically, this means the following (be sure to replaces the Xs with a unique and strong password of your own):
create user 'omeka'@'localhost' identified by 'type password here';

create database omeka;

grant all privileges on omeka.* to 'omeka'@'localhost';

show databases;

\q


***Setup db.ini

---

In the extracted directory, find the db.ini file and add your database credentials, and replace all values containing XXXXXX, with the appropriate information. This is the same thing we did with the login.php file for our bare bones OPAC/ILS and the wp-config.php file for WordPress.
Follow these general steps:

Change to the omeka directory, if you haven't already.

Copy and rename the db.ini file to db.ini-original.

Edit the file and add your Omeka database name, user name, and password in the fields for DB_HOST, DB_USERNAME, DB_PASSWORD, AND DB_NAME.

This means that we specifically do the following:

cd /var/www/html/omeka

sudo cp db.ini db.ini-original

sudo nano db.ini

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; Database Configuration File ;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;
; Omeka requires MySQL 5 or newer.
;
; To configure your database, replace the X's with your specific
; settings. If you're unsure about your database information, ask
; your server administrator, or consult the documentation at
; <http://omeka.org/codex/Database_Configuration_File>.

[database]
host     = "XXXXXXX"
username = "XXXXXXX"
password = "XXXXXXX"
dbname   = "XXXXXXX"
prefix   = "omeka_"
charset  = "utf8"
;port     = ""


host     = "localhost"
username = "libdis"
password = "type password here"
dbname   = "omeka"
prefix   = "omeka_"
charset  = "utf8"
;port     = ""

Additionally, we want to disable FTP uploads to the site. To do that, navigate to the end of the file and add the following line:
define('FS_METHOD','direct');

Source of git code repo above: https://github.com/omeka/Omeka/blob/94acbc29ad05b38e7103bfa34d75a3c8c937a7f5/db.ini.changeme
More Omeka code repositories: https://github.com/omeka/Omeka


***Change Ownership

---

Use the chown command like we did with WordPress on the files directory in the omeka directory. The user and owner should again be www-data
Omeka will need to write to files in the base directory. Assuming you’re still in your base directory, /var/www/html/omeka, run the following command:

From bbilz@syslib-2023:/var/www/html/omeka#

sudo chown -R www-data:www-data *


***Security

---

Since our HTML and PHP files allow us to enter data into our MySQL database from a simple web interface, we need to limit access to the module. Again, in a real-world situation, modules like these would have a variety of security measures in place to prevent wrongful data entry. In our case, we will rely on a simple authorization mechanism provided by the Apache2 server called htpasswd.

First, we create an authentication file in our /etc/apache2 directory, which is where the Apache2web server stores its configuration files. The file will contain a hashed password and a username we give it. In the following command, I set the username to libdis, but it could be anything:
sudo htpasswd -c /etc/apache2/.htpasswd libdis

Next we need to tell the Apache2 web server that we will use the htpasswd to control access to our cataloging module. To do that, we use nano to open the apache2.conf file. We need
sudo nano /etc/apache2/apache2.conf

In the apache2.conf file, look for the following code block / stanza. We are interested in the third line in the stanza, which is line 173 for me, and probably is for you, too.

<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride None
  Require all granted
</Directory>

Carefully, we need to change the word None to the word All:

<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>

Next, change to the omeka directory and use nano to create a file called .htaccess (note the leading period):

cd /var/www/html/omeka

sudo nano .htaccess

Add the following content to .htaccess:
AuthType Basic

AuthName "Authorization Required"

AuthUserFile /etc/apache2/.htpasswd

Require valid-user

Check that the configuration file is okay:

apachectl configtest

If you get a Syntax OK message, then restart Apache2 and check its status:

***Restart Apache2 and MySQL

---

sudo systemctl restart apache2

sudo systemctl restart mysql

Now visit your omeka module. You should be required to enter the username and password that you created with htpasswd.


***Run the Install Script

---

In your web browser, go to http://74.70.197/240/omeka/ and complete the setup via the web form, just like you did with WordPress

The next part of the process takes place in the browser. The location (URL) that you visit in the browser depends on your specific IP address and also includes the directory in /var/www/html that we extracted Omeka to or that you renamed if you followed Step 5. I renamed omeka-3.1 to omeka, then I need to visit the following URL:

http://34.70.197.240/omeka/wp-admin/install.php


***Finishing Installation

---

From this point forward, the steps to complete the installation are exactly the steps you follow using WordPress's documentation.

Most importantly, you should see a Welcome screen where you enter your site's information. The site Username and Password should not be the same as the username and password you used to create your WordPress database in MySQL. Rather, the username and password you enter here are for Omeka users; i.e., those who will add content and manage the website.

Two things to note:

We have not setup Email on our servers. It's actually quite complicated to setup an email server correctly and securely, but it wouldn't work well without having a domain name setup anyway. So know that you probably should enter an email when setting up the user account, but it won't work.
Second, when visiting your site, your browser may throw an error. Make sure that the URL is set to http and that it's not trying to access https. Setting up an https site also generally requires a domain name, but we are not doing that here. So if there are any problems accessing your site in the browser, be sure to check that the URL starts off with http.
