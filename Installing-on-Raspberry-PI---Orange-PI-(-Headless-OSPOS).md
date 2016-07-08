# Installation of Basic Components

Login to your pi pi ssh using Putty.
First update all the packages.  

`sudo apt-get update` & `sudo apt-get upgrade`
  
Become root `sudo su`  

Then install Apache, PHP, MySQL in and phpMyAdmin order to be able to run OSPOS.  

 `sudo apt-get install apache2 php5 libapache2-mod-php5 mysql-server php-pear php5-mysql phpmyadmin apache2-utils php5-gd php5-intl -y`

Add the user name and password for MySQL and phpMyAdmin.


## Configuration

Configure Date and Time according to your location for the server to run correctly.

1. `sudo dpkg-reconfigure tzdata` Select your time Zone Modify the PHP files for the Time zone.

2. goto `nano /etc/php5/cli/php.ini ` and find "Date" by scrolling down or by Ctrl+W and remove ; from the line and modify like this `date.timezone = Asia/Kolkata`.

3. goto `nano /etc/php5/apache2/php.ini ` and find "Date" by scrolling down or by Ctrl+W and remove ; from the line and modify like this `date.timezone = Asia/Kolkata`.
  
4. Modify Apache 2 for the PHPMYADMIN.
   goto `nano /etc/apache2/apache2.conf` and Add the next code to the bottom of the line `Include /etc/phpmyadmin/apache.conf`.

5. restart Apache and check if it's working correctly `/etc/init.d/apache2 restart`.


### Installing And Configuring OSPOS (must be root)

1. Download OSPOS `git clone https://github.com/jekkos/opensourcepos `.  

2. Rename PHP file `cp -r opensourcepos/application/config/database.php.tmpl opensourcepos/application/config/database.php`.  
3.Modify application/config/database.php to connect to your database.  
`nano opensourcepos/application/config/database.php`.  
go to the bottom of the file and modify this to your database  

`$db['default'] = array(
        'dsn'   => '',
        'hostname' => 'localhost',
        'username' => 'root',
        'password' => '12345678',
        'database' => 'opensourcepos',
`

4. Copy This Files to apache.  
`cp -r opensourcepos /var/www/html`
5. Change the permissions  
`chmod -Rv 755 cache* /var/www/html/opensourcepos`.  
6. Restart Apache  
`/etc/init.d/apache2 restart`.

#### Configuring OSPOS ( Network Install )
Please do not use a Web Browser with a lot of addons as it can create problems with OSPOS.
Install Firefox if your are using Chrome with a lot of addons.

1. Download the Source form `https://github.com/jekkos/opensourcepos`.
2. Go to your PI's ip address e.g `http://192.168.3.116/phpmyadmin`. 
3. Create a database name as above saved in configuration file.
4. As it's a local installation to improve performance set in application/config/config.php $config['ospos_xss_clean'] = FALSE; - Please note that this will disable the Cross Site Scripting protection, but assuming it's a standalone installation you should not have this issue -
5. Select that Database and Click import and select the database file from previously downloaded file.
6. After successfully importing the database login to OSPOS.
7. Restart apache `/etc/init.d/apache2 restart`
8. Go to your PI's ip address e.g `http://192.168.3.116/opensourcepos`. 
9. Enjoy!!!.

