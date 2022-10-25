# <div align="center"> Installing a LEMP Stack in AWS / Project-2 </div>
#### LEMP is an open-source web application stack used to develop web applications. The term LEMP is an acronym that represents L for the Linux Operating system, NGINX (pronounced as engine-x, hence the E in the acronym) web server, M for MySQL database, and P for PHP scripting language.
___
###### * This project has a prerequistie of creating an Ubuntu EC2 instance on my personal AWS account. That instance has a security policy attached which allows me to log into it using SSH on port22 from my local laptop. The creation and setup of this instance is not documented here. 

__Step 1__ – Installing the Nginx Web Server
After logging in to the new Ubuntu server from my local Windows terminal, I performed the following commnads to install NGINX
```
sudo apt update               # upate the servers package index
sudo apt install nginx        # install NGINX
```

![updatepackageindex](./images/packageindex.PNG)
__Confirm install by answering "y"__
![Nginxconfirnm](./images/nginxconfirminstall2.PNG)
__When the install procedure returns to the console prompt.. I ensure NGINX is active ---> See the green text active (running) status__
![Nginxrunning](./images/nginxrunning2.PNG)

###### * I have edited my security group to allow inbound connections on HTTP TCP port 80 which is the default port that web browsers use to access web pages on the Internet.

First, I check if i can access my NGINX server locally from my Ubuntu shell using the command.
```
curl http://127.0.0.1:80
```
My NGINX web service responds to the ‘curl’ command with some payload.
![Nginxresponds](./images/nginxresponds.PNG)

Now it is time for me to test if my NGINX server can respond to requests from the Internet.
From my web browser I try to access the NGINX server with the following url
```
http://<Public-IP-Address>:80
```
I can find the public ip address of my web server with the following command from the console
```
curl -s http://169.254.169.254/latest/meta-data/public-ipv4
```
And use that IP address in my URL as follows:
![EnterinBrowser](./images/browserpublicip.PNG)
My new NGINX server is responding to my requests over the Internet made from my local browser.
![RespondsOverInternet](./images/respondsoverinternet.PNG)

___
### <div align="center"> Step 2) Installing MySQL </div>

Now that I have a web server up and running, I need to install a Database Management System (DBMS) to be able to store and manage data for my site in a relational database. MySQL is a popular relational database management system used within PHP environments, so I will use it in my project.
I use ‘apt’ run from the SSH session to acquire and install this software:
```
sudo apt install mysql-server
```
![InstallSQL](./images/Installmysqlserver.PNG)
I then check if SQL is up and running after the install with the command
```
systemctl status mysql
```
![SQL-running](./images/sqlrunning.PNG)
Now i am able to login as root (which is inferred by the use of sudo) to the Mysql server from the remote console <br/>
At this time I will also set a password for the root user using the following commands

```
sudo mysql
```
This brings me to a mysql> prompt on the console
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '******';
```

![login-SQL](./images/loginandsetpassword.PNG)
I then exit the mysql shell with the exit command
```
mysql> exit
```
At this point it is recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system <br/>
In most of the configurations presented I provided the most restrictive responses
![SQL-secure](./images/sqlsecurityscript.PNG)

Now I test to see if i can log into mysql console with the previously configured password utilizing the ALTER USER command
```
sudo mysql -p
```
![SQL-login](./images/lognsqlwithpassword.PNG)
I am able to successfully login to my SQL server with the configured password
___
### <div align="center"> Step 3) Installing PHP </div>
I’ll need to install php-fpm, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. 
In addition I will also need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. 
*PHP-FPM includes numerous features that can prove beneficial for websites receiving traffic in large volumes frequently*

To install these 2 packages at once, I will run:

```
sudo apt install php-fpm php php-mysql
```

When the PHP install is cmopletted, I run the following command to confirm my PHP version:
```
php -v
```
![PHP-version](./images/installphpandversion.PNG)
___


### <div align="center"> Step 4) Creatring a virtual host for my website using Apache </div>
To test my setup with a PHP script, I will set up a proper Apache Virtual Host to hold my website’s files and folders. Virtual host allows me to have multiple websites located on a single machine and users of my websites will not even notice it. (illistrated below) <br/>
![VirtualHost](./images/VirtualHost.png)

I will create the directory for my lamproject using ‘mkdir’ command as follows:
```
sudo mkdir /var/www/lampproject                          ### Ceate Web dcoument directory
sudo chown -R $USER:$USER /var/www/lampproject           ### Assign ownership of new Web docuemnt directory to curent system user
sudo vi /etc/apache2/sites-available/lampproject.conf    ### Create new configuration for for Apaches sites-availalble
```
Contents of new configuraion file - lampproject.conf
```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp------------------- ### This line configures my new directory as Apache's web root directory
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Now I use the following set of commands to enable my new virtual host and disable Apaches default website and then reload apache.
```
sudo a2ensite lampproject                                ### 
sudo a2dissite 000-default                               ###
sudo apache2ctl configtest                               ###  make sure my configuration file doesn’t contain syntax errors
sudo systemctl reload apache2                            ###
```

Now I will create an index.html file in my /var/www/projectlamp folder so that I can test that the virtual host works as expected:

```
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' <br/> 
$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
```
My Apache virtual host is working as expected. I can access it from my local machines browser using it's DNS name.
![VirtualHostWorking](./images/websitefrombrowser.PNG)

___
### <div align="center"> Step 5) Enable PHP on my website </div>
Modify the /etc/apache2/mods-enabled/dir.conf in order to change Apache's default behavior which is to load an html file over a php file <br/>
and restart apache 
```
<IfModule mod_dir.c>
                DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
I create a new index.php file in my custonm web root folder and add teh following code
_vim /var/www/projectlamp/index.php_
```
<?php
phpinfo();
```

Finally , the browser renders the following page which provides inforamtion about my server from the perspective of PHP.

![PHPPageWorking](./images/phppagerendered.PNG)
