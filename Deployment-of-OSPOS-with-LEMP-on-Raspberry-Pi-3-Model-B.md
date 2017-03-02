**Default Linux, Nginx, MariaDB, PHP7.0 & Adminer stack on Raspbian Jessie.**

# 1. Add New Source Repository 

By default Raspbian Jessie comes with PHP5.6, so you have to add a new repo to use php7. 
You can use php5.6 but php7 performs far better.

### Type the following code in your terminal:

`sudo nano /etc/apt/sources.list`

### Add this line to the list:

`deb http://mirrordirector.raspbian.org/raspbian/ stretch main contrib non-free rpi`

Save the file by pressing **Ctrl+x, y, Enter**.

# 2. Update Raspbian Jessie

`sudo apt-get update`

`sudo apt-get upgrade`

# 3. Install Nginx Web Server

`sudo apt-get install nginx`

`sudo systemctl enable nginx`

`sudo systemctl start nginx`

`systemctl status nginx`

Now in your browser’s address bar, type `http://localhost` or `http://127.0.0.1` and hit enter

You will see "Welcome to nginx!, that means nginx installed and running successfully.

Now, we need to make www-data (Nginx user) as the owner of web root directory

`sudo chown www-data /var/www/html -R`

# 4. Install MariaDB

`sudo apt-get install mariadb-server mariadb-client`

MariaDB will ask you to set root user's password, provide it and confirm it.

`sudo systemctl enable mysql`


# 5. Install PHP7

`sudo apt-get install php7.0-fpm php7.0-mbstring php7.0-mysql php7.0-common php7.0-gd php7.0-cli php7.0-curl php7.0-intl php7.0-bcmath php7.0-mcrypt`

`sudo systemctl start php7.0-fpm`

`systemctl status php7.0-fpm`

# 6. Create a Default Nginx Server Block File

### Remove the "default.conf" symlink in "sites-enabled" directory

`sudo rm /etc/nginx/sites-enabled/default`

### create a new default server block file under /etc/nginx/conf.d/ directory

`sudo nano /etc/nginx/conf.d/default.conf`

### Paste the following text into the file, save and close the file


server {
		server_name localhost;
		root /var/www/html/;
		index index.php index.html index.htm;

		location / {
			try_files $uri $uri/ /index.php;
		}
    
		location /opensourcepos {
			try_files $uri $uri/ /opensourcepos/public/index.php;
		}
	
		location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|xml)$ {
			expires  15d;
		}

		location ~ \.php$ {
			include /etc/nginx/fastcgi_params;
			fastcgi_index  index.php;
			fastcgi_param  SCRIPT_FILENAME  /var/www/html/$fastcgi_script_name;
			fastcgi_param  REQUEST_URI      $request_uri;
			fastcgi_param  QUERY_STRING     $query_string;
			fastcgi_param  REQUEST_METHOD   $request_method;
			fastcgi_param  CONTENT_TYPE     $content_type;
			fastcgi_param  CONTENT_LENGTH   $content_length;
			fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
		}
	}



### Test nginx configuration and reload it

`sudo nginx -t`

`sudo service nginx restart`


# 7. Test PHP

`php --version`

**Test PHP-FPM, create a php_info.php file in the Web root directory**

`sudo nano /var/www/html/php_info.php`

Paste the following code to the file:

`<?php phpinfo(); ?>`

Now in the browser address bar, enter `localhost/php_info.php`. You should see your server’s PHP information. This means PHP is workinging fine. For your server’s security, you should delete `php_info.php` file now.


# 8. Install 'Adminer'

Download Adminer from this page:

https://www.adminer.org/

Place it in var/www/html folder. To access it, type in your browser `localhost/adminer-x.x.x.php`

**NOTE:** x.x.x stands for Adminer version, you have downloaded.


# 9. Deploy OSPOS

Now download, extract and place `opensourcepos` to var/www/html. 
Don't forget to rename it as **opensourcepos**.
Create a new Database using Adminer.
Rename your Application/config/database.php.tmpl to **database.php**.
Provide database connection credentials by editing the **database.php** file.
Type in your browser `http://localhost/opensourcepos/public`.


**ENJOY!**

If you have any issue, please post in the **Issues** section.




