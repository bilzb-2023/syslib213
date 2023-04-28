# Week 9: Create a Bare Bones Cataloging Module

---

## Task

1. Create an index.html file in a new cataloging directory in /var/www/html
2. Create an insert.php file in the new cataloging directory
3. Secure your cataloging directory with the htpasswd command
4. Add some additional records using the new web form
5. Use the OPAC to retrieve the new records
6. Post screenshots in Canvas.


---


### Creating the HTML Page and a PHP Cataloging Page

1. Create a new directory

cd /var/www/html
sudo mkdir cataloging

2. Create an index.html file in a new cataloging directory in /var/www/html

cd cataloging
sudo nano index.html

3. Insert this text in the index.html file

<!DOCTYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>

    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>

    <form action="insert.php" method="post">
        <label for="author">Author:</label>
        <input type="text" name="author" id="author" required><br><br>

        <label for="title">Book Title:</label>
        <input type="text" name="title" id="title" required><br><br>

        <label for="publisher">Publisher:</label>
        <input type="text" name="publisher" id="publisher" required><br><br>

        <label for="copyright">Copyright:</label>
        <input type="date" id="copyright" name="copyright">

        <input type="submit" value="Submit">
    </form>
</body>
</html>


### PHP Insert Script

1. Create an insert.php file in the new cataloging directory using nano

<?php

// Load MySQL credentials
require_once '../login.php';

// Establish connection
$conn = mysqli_connect($db_hostname, $db_username, $db_password) or
  die("Unable to connect");

// Open database
mysqli_select_db($conn, $db_database) or
  die("Could not open database '$db_database'");

// Prepare and bind SQL statement
$stmt = $conn->prepare("INSERT INTO books (author, title, publisher, copyright) VALUES (?, ?, ?, ?)");
$stmt->bind_param("ssss", $author, $title, $publisher, $copyright);

// Set parameters and execute statement
$author = $_POST["author"];
$title = $_POST["title"];
$publisher = $_POST["publisher"];
$copyright = $_POST["copyright"];

if ($stmt->execute() === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $stmt->error;
}

// Close statement and connection
$stmt->close();
$conn->close();

echo "<p>Return to the cataloging page: <a href='http://==34.70.197.240==/cataloging/'>http://==34.70.197.240==/cataloging/</a></p>";
?>


**Be sure to change the url for the cataloging page**


### Security

1. Create an authentication file in **/etc/apache2** directory

**sudo htpasswd -c /etc/apache2/.htpasswd libcat**

2. Tell the Apache2 to use **htpasswd** to control access to the cataloging module.

**sudo nano /etc/apache2/apache2.conf**

3. Update the **apache2.conf** file

Change **None** to **All**

<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride **~~None~~** to **All**
  Require all granted
</Directory>


4. Change to the **cataloging** directory and use **nano** to create a file called **.htaccess**

cd /var/www/html/cataloging
sudo nano .htaccess

5. Add this text to **.htaccess**

AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user

6. Check configuration

**apachectl configtest**

7. If message says **Syntax OK**, restart Apache2 and check status

**sudo systemctl restart apache2
systemctl status apache2**

8. Visit the cataloging module which should require the username and password to be entered
