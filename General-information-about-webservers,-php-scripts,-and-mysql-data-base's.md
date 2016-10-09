Because there are users who need additional information about these things, I will in my spare time answer all the questions that come up in issues that are not an OSPOS issue.

how to use cpanel,
how to move or backup mysql,
how to move your webserver,
More later,

php and other scripts need a webserver and in most cases a mysql database to use and run them. If you do not have a webserver hosted at one of the many webhosts out there then you will need to have a webserver (Windows: Apache + MySQL + PHP & more) running on your local computer, like Xampp, wamp or my favorite, http://www.uniformserver.com/  

## What version of php am I running?
Load this file (info.php) in your public_html folder, then run the script, mywebsite.com/info.php
copy this code 

`<?php
// Show all information, defaults to INFO_ALL
phpinfo();
?>` 

to notepad and save as All Files (*.*) named info.php

you can find more information here: http://php.net/manual/en/function.phpinfo.php

## Moving your files and system to new local computer?

If you use Uniform Server then all that is needed to move your system is just backup and move your files. It is the biggest reason I use portable apps (http://portableapps.com/apps/) in the first place. I will have to do more research on moving other servers.

## Using Uniform Server

Uniform Server (http://www.uniformserver.com/) ZeroXIII releases are versions with pre-installed
 ZeroXIII modules producing a standard WAMP (Windows, Apache, MySQL 
 and PHP) server package. After extracting, servers are ready to
 run either from a USB memory stick or PC. Apart from changing
 the MySQL password (optional) there is no configuration required.

Uniform Server uses 7z self-extracting archives. Archives are
 compressed using 7z and include the 7-Zip extractor. To unpack
 double click on the exe file this unpacks all folders and files
 contained in the archive nothing is added to the registry or
 installed. If you wish to view and extract individual
 folders/files download 7-z portable from:
 http://portableapps.com/apps/utilities/7-zip_portable
