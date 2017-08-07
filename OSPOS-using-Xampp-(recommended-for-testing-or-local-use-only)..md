**If you are using WAMP follow the MAMP setup for the icu files.**

Make sure the version you use does not use mysql 5.7. It currently does not work with OSPOS.
Currently Php 7 is working.
Download and Install Xampps currrent version for 3.1.0 or an earlier version of Xampp for 3.0.2. OSPOS is working great on Windows 10.
https://www.apachefriends.org/download.html
Launch the Control Panel.
Start Apache and Mysql.
From Apache select Config.
Edit the Php.ini file to uncomment the following extensions as needed. The extensions are about halfway down.
bcmath already appears to be enabled in this version of Xampp.

extension=php_gd2.dll, This may already be enabled.

extension=php_intl.dll, Was not enabled.

extension=php_sockets.dll. Was not enabled.

Now Apache should be ready to go.

**Download and extract either Stable or Unstable from the Readme page.**

**If you are using Windows right click on the downloaded zip file.**

**Select properties and Select the Unblock button if it is there. Then extract the file.**

**Place the extracted file into the htdocs directory.**

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

**Restart the Apache server after you have made any changes.**

Now you should be able to go to localhost/what ever name you chose to use/public and see the login screen.  
Default user - admin  
Default password - pointofsale.  
Play around and get familiar with OSPOS.