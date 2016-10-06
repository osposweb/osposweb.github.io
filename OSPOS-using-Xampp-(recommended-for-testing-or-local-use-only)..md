Current version of Xampp includes:
Includes: Apache 2.4.23, MariaDB 10.1.16, PHP 7.0.9, phpMyAdmin 4.5.1, OpenSSL 1.0.2, XAMPP Control Panel 3.2.2, Webalizer 2.23-04, Mercury Mail Transport System 4.63, FileZilla FTP Server 0.9.41, Tomcat 7.0.56 (with mod_proxy_ajp as connector), Strawberry Perl 7.0.56 Portable

Make sure the version you use does not use mysql 5.7. It currently does not work with OSPOS.

Download and Install Xampp - Version 7.0.9 / PHP 7.0.9 it is working great on Windows 10.
https://www.apachefriends.org/download.html
Launch the Control Panel.
Start Apache and Mysql.
From Apache select Config.
Edit the Php.ini file to uncomment the following extensions.Extensions are about halfway down.
bcmath already appears to be enabled in this version of Xampp.
[bcmath]
; Number of decimal digits for all bcmath functions.
; http://php.net/bcmath.scale
bcmath.scale=0,
extension=php_gd2.dll,
extension=php_intl.dll,
extension=php_sockets.dll.
Now Apache should be ready to go.

Download and extract https://github.com/jekkos/opensourcepos.
Place the extracted file into the htdocs directory.

In Xampp Control Panel go to Mysql - Admin.
Create a new database. Name it ospos or whatever you want.
Now select the database and go to import.
Select browse and go to the opensourcepos directory and locate the database directory.
Select database.sql for the import if this is a new install.
Select 2.4_3.0.sql for the import if this is an updated install.
After the database has completed installing go back to the ospos dir and go to ospos/application/config. 
Rename database.php.tmpl to database.php.
Open database.php and change the following lines as needed.  
'username' => '',default name is root for mysql.  
'password' => '',default no password for mysql or change if you created a mysql password.  
'database' => '',change this to your new database name.    
Edit and save.

Now you should be able to go to localhost/opensourcepos/public and see the login screen.  
Default user - admin  
Default password - pointofsale.  
Play around and get familiar with OSPOS.