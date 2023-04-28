# Week 7: Install the LAMP Server

---

## Task

1. Learn how to set up a LAMP (Linux, Apache, MySQL, PHP) stack.

This stack enables us to create a web server that provides extra funtionality via PHP and MySQL, both of which are required to run content management systems and integrated library systems.


### Installing the Apache Web Server


1. Update the systems first:  **sudo apt update**

2. **sudo apt -y upgrade**

3. Install Apache2 using **apt**. Use **apt search** to identify the specific package name. I already know that a lot of results will be returned, so let's pipe the **apt search** command through **head** (top 10 lines in a file) to look at the initial results:

**sudo apt search apache2 | head**

The package that we're interested in happens to be named **apache2** on Ubuntu. This package name is not a given since on other distributions, like Fedora, the Apache package is called **httpd**. To learn more about the apache2 package, use the **apt show** command:

**apt show apache2**

Once we've confirmed that apache2 is the package that we want, we install it with the **apt install** command. Press Y to agree to continue after running the command below:

**sudo apt install apache2**


### Basic checks

1. Make sure the server is up and running, configure some basic things, and then create a basic web site.

2. To start, let's use **systemctl** to acquire some info about apache2 and make sure it is enabled and running:

- **systemctl list-unit-files apache2.service**
- **systemctl status apache2**

- The output shows that apache2 is enabled, which means that it will start running automatically when the computer gets rebooted.

- The output of the second command also shows that apache2 is active, which means that it has started working.


### Creating a web page

Since **apache2** is up and running, look at the default web page.

There are two ways we can look at the default web page. We can use a command line web browser. There are a number available, but Dr. Burns likes **w3m**.

Also use regular web browsers and view the site by entering the IP address of the server in our browser URL bar.

To check with **w3m**, install it first using these commands:

- **sudo apt install w3m**

Once it's installed, we can visit the default site using the loopback IP address (aka, localhost). From the command line on our server, we can run either of these two commands:

1. **w3m 127.0.0.1**

2. **w3m localhost**

We can also get the subnet/private IP address using the ip a command, and then use that with **w3m**. For example, if ip a showed that my NIC has an IP address of **10.0.1.1**, then use **w3m** with that IP address:

- **w3m 10.0.1.1**

If the **apache2** installed and started correctly, then should see the following text at the top of the screen:

**Apache2 Ubuntu Default Page**
**It works!**

To exit **w3m**, press **q** and then **y* to confirm exit.

Note: I wrote **"press q to exit"** at twice in my notes as a reminder.

---

To view the default web page using a regular web browser (e.g., Firefox, Chrome, Safari, Edge), go to the server's public IP address. To do that, log into the Google Cloud Console. In the left hand navigation panel, hover your cursor over the **Compute Engine** link, and then click on **VM instances**. You should see your **External IP** address in the table on that page. You can copy that external IP address or simply click on it to open it in a new browser tab. Then you should see the graphical version of the **Apache2 Ubuntu Default Page**.

---

> Note that most browsers nowadays may try to force HTTPS mode, and they also often hide the protocal from the URL. If the web page is not loading, make sure the URL is **http://IP-ADDRESS** and *not* https://IP-ADDRESS.

---

Please take a moment to read through the text on the default page. It provides important information about where Ubuntu stores configuration files and what those files do, and the document root, which is where website files are stored.


### Create a Web Page

Let's create a web page. The default page described above provides the location of the document root at **/var/www/html**. When we navigate to that location on the command line, we'll see that there is already an **index.html** file located in that directory. This is the **Apache2 Ubuntu Default Page** that we visited above in our browsers. Let's rename that **index.html** file, and create a new one:

> **cd /var/www/html/**

> **sudo mv index.html index.html.original**

> **sudo nano index.html**

---

Note: we use **sudo** in this directory because we are working on files and directories outside our home directories. Thus, be careful here about the commands you run. Any mistake may result in deleting necessary files or directories.

---

If I know HTML, then write some basic HTML code to get started. Otherwise, re-type the content below in nano, and then save (^O) and exit out (^X).

<html>
<head>
<title>My first web page using Apache2</title>
</head>
<body>

<h1>Welcome</h1>

<p>Welcome to my web site.

I created this site using the Apache2 HTTP server.</p>

</body>
</html>


If the site is open in the web browser, reload the page, should see the new text.

I can still view the original default page by specifying its name in the URL. Remember that web browsers are, at their most basic, simply file viewers. So it makes sense that one simply has to specify the name of the file one wants to view. For example, if your **external IP address** is **34.70.197.240**, then specify it like so:

<http://==34.70.197.240==/index.html.original>

---

### Conclusion

In this section, we learned about the Apache2 HTTP server. We learned how to install it on Ubuntu, how to use systemd (systemctl) commands to check its status, how to create a basic web page in /var/www/html, how to view that web page using the w3m command line browser and our regular graphical browser,

In the next section, we will install PHP, which will provide the language needed to connect to MySQL, and thus enable more data driven web sites.
