# INSTALL LAMP STACK ON AWS - UBUNTU 20

Step 1 — Installing Apache and Updating the Firewall
```
	sudo apt update -y
	sudo apt upgrade -y
	sudo apt install apache2 -y
```
 APACHE INSTALLED SUCCESFULLY TILL HERE, YOU CAN CHECK BY ENTERING YOUR PUBLIC IP OR PUBLICK DNS ADDRESS 
- http://your_server_ip


Step 2 — Installing MySQL

```
sudo apt install mysql-server
```

```
sudo mysql_secure_installation
```

```
sudo mysql
```

```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

Note  please note here replace the "password" with yours.

```

GRANT ALL PRIVILEGES ON database-name .* TO 'root'@'localhost' IDENTIFIED BY 'password';

```
```
FLUSH PRIVILEGES;
```

```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```
```
exit
```

At this point, your database system is now set up and you can move on to installing PHP, the final component of the LAMP stack.

Step 3 — Installing PHP

```
sudo apt install php libapache2-mod-php php-mysql
```

In most cases, you will want to modify the way that Apache serves files when a directory is requested. Currently, if a user requests a directory from the server, Apache will first look for a file called index.html. We want to tell the web server to prefer PHP files over others, so make Apache look for an index.php file first.

```
sudo nano /etc/apache2/mods-enabled/dir.conf
```
Move the PHP index file (highlighted above) to the first position after the DirectoryIndex specification, like this:
```
<IfModule mod_dir.c>
	DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>	
```

```
sudo systemctl restart apache2
sudo systemctl status apache2
```

Press Q to exit this status output.
	
Check PHP Version by entering 
```
 php -v
```

	Install the commonly required php modules by using the below commands - do remeber replace the php version number with your by checking the php -v command 
	For Example if the php -v command shows 7.4 version installed then you have to replace the 7.2 with 7.4 in the below command


```
sudo apt install php7.2-common php7.2-mysql php7.2-xml php7.2-xmlrpc php7.2-curl php7.2-gd php7.2-imagick php7.2-cli php7.2-dev php7.2-imap php7.2-mbstring php7.2-opcache php7.2-soap php7.2-zip php7.2-intl -y
```
```
	sudo systemctl restart apache2
```

	
Step 4 — Testing PHP Processing on your Web Server
```
sudo nano /var/www/html/info.php
```	

#This will open a blank file. Add the following text, which is valid PHP code, inside the file:


```
<?php
phpinfo();
?>

```	
The address you will want to visit is:

	http://your_ip/info.php

You will get the php info page

Step 1 — Installing phpMyAdmin

```
sudo apt update
sudo apt install phpmyadmin php-mbstring

```
Warning: When the prompt appears, “apache2” is highlighted, but not selected. If you do not hit SPACE to select Apache, the installer will not move the necessary files during installation. Hit SPACE, TAB, and then ENTER to select Apache.
```
sudo phpenmod mbstring
sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
sudo a2enconf phpmyadmin
sudo systemctl restart apache2
```

  
Step 2 — Adjusting User Authentication and Privileges
```
  sudo mysql
```
```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
```
FLUSH PRIVILEGES;

```
```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

You can now access the web interface by visiting your server’s domain name or public IP address followed by /phpmyadmin:

http://your_domain_or_IP/phpmyadmin


	
