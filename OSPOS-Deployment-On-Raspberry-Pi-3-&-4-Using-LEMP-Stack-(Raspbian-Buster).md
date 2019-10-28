**Default Linux, Nginx, MariaDB, PHP7.3 & Adminer stack on Raspbian Buster.**

# 1. Updating Software Packages

Update repository and software packages. Run the following commands on terminal:

### Type the following code in your terminal:

`sudo apt update`
`sudo apt update`

# 2. Installing Nginx Web Server

Nginx is a web server which can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache. Nginx is best suited for Raspberry Pi installations due to its light-weight resource utilization and its ability to scale easily on minimal hardware.

`sudo apt install nginx`

To enable Nginx at boot automatically, run:

`sudo systemctl enable nginx`

Although Nginx will most probably be running, you can explicitly start it using:

`sudo systemctl start nginx`

Check Nginx Status by running the following command:

`systemctl status nginx`

Check, if Nginx is successfully installed by typing localhost or 127.0.0.1 in your browser. If a "Welcome To nginx!" screen shows up, Nginx installation was successful.

Now, we need to set www-data (Nginx user) as the owner of web root directory, we can achieve this by using the chown command:

`sudo chown www-data /var/www/html -R`

# 3. Installing MariaDB Database Server

MariaDB is currently offering better performance as compared to MySQL and it is used as a drop-in replacement for MySQL.

`sudo apt install mariadb-server mariadb-client`

After installation, check MariaDB status by typing:

`systemctl status mariadb`


To enable MariaDB at boot automatically, run:

`sudo systemctl enable mariadb`

Now run the secure installation script by typing:

`sudo mysql_secure_installation`

You will be prompted to enter the password for 'root', just hit Enter as the password is not set yet. 

Now, you will be prompted to add a password for 'root', Enter 'Y' and set password.

For the next few questions, just hit Enter until the process finishes.


# 4. Installing PHP7.3 on Debian 10

PHP 7.3 has noticeably better performance than prevoius versions, as far better performance than PHP 5. Get the required PHP extensions by typing:

`sudo apt install php7.3 php7.3-fpm php7.3-mysql php-common php7.3-cli php7.3-common php7.3-json php7.3-opcache php7.3-readline`

Also, get the following PHP modules:

`sudo apt-get php7.3-bcmath php7.3-intl php7.3-gd php7.3-mbstring php7.3-curl php7.0-mcrypt`

Run the following commands to enable PHP at startup and start PHP:

`sudo systemctl enable php7.3-fpm`

`sudo systemctl start php7.3-fpm`

To verify your installation you can check your PHP version by typing:

`php --version`



# 5. Creating a Nginx Server Block

### Remove the default symlink in sites-enabled directory because thedefault server block is inadequate to run PHP code. Run the following command to remove it:

`sudo rm /etc/nginx/sites-enabled/default`

### Create a new server block file under /etc/nginx/conf.d/ directory with Nano.

`sudo nano /etc/nginx/conf.d/default.conf`

### Paste the following text into the file, save and close the file
```
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
			fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
		}
	}
```

Press Ctrl+O to write changes to the file and then hit Enter to confirm. Then exit Nano by pressing Ctrl+X.

### Test Nginx configuration and then reload it:

`sudo nginx -t`

`sudo systemctl reload nginx`


# 7. Testing PHP

**Test PHP-FPM, create a test.php file in the Web root directory**

`sudo nano /var/www/html/test.php`

Paste the following code to the file:

`<?php phpinfo(); ?>`

Press Ctrl+O to write changes to the file and then hit Enter to confirm. Then exit Nano by pressing Ctrl+X.

Now type the following in your browser's address bar `localhost/test.php`. You should see your server’s PHP information. This means PHP scripts can run properly with Nginx web server. 

# 8. Install 'Adminer'

Download the latest release Adminer from the following URL:

https://www.adminer.org/

Copy Adminer to var/www/html folder by typing (make sure you enter your username in the path):

`sudo cp /home/your_username/Downloads/adminer-x.x.x.php /var/www/html`

To access Adminer, type in your browser `localhost/adminer-x.x.x.php`

**NOTE:** x.x.x stands for Adminer version, you have downloaded.

You might face this error while logging in to adminer: **'Access denied for user 'root'@'localhost'**. Follow the following steps:

`sudo systemctl stop mariadb`

Start the database without loading the grant tables or enabling networking:

`sudo mysqld_safe --skip-grant-tables --skip-networking &`

Now you can connect to the database as the root user, which should not ask for a password.

`mysql -u root`

Execute the following query(make sure to replace new_password with your password):

`ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';`

You should see confirmation that the command has been successfully executed. Now exit and restart MariaDB;

`exit;`

`sudo systemctl start mariadb`


# 9. Deploy OSPOS

Now download the latest release of OSPOS from: 
`https://github.com/opensourcepos/opensourcepos/releases`

Extract and place `opensourcepos` to var/www/html. 
Don't forget to rename it as **opensourcepos** (Don't change the name to anything else).
Create a new Database named **'ospos'** using Adminer.
Create a new user named **'admin'**(if not already present) with password **'pointofsale'**.
You can also provide your own database connection credentials by editing the **database.php** file as configuring adminer accordingly.
Type the URL in your browser `http://localhost/opensourcepos/public`.
If everything is successful, you should now see the Login page.
Login with the user 'admin' with password 'pointofsale' or your own edited credentials in database.php file.

**ENJOY!**

If you have any issue, please post in the **Issues** section.