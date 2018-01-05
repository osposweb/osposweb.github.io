## Overview
_Work in progress_
When user input isn't correct OSPOS will normally respond with an error message included with the response to the Web page.

However, if you are trying to chase down something that is causing a more serious issue then you might need more information from the system. You will need to activate and/or take advantage one of the handful of error logs that OSPOS or the supporting platforms generate.

## PHP Errors

If the error is due to something going haywire in the application code then you might need to activate the PHP error log.

There are two aspects to it.  The first is identifying where the log is to be created and the second is establishing what should be written to the log.  OSPOS also provides the option of display errors directly to the user in the Web page but that will can make the Web page wonky (but sometimes it is a good thing to be wonky).   To have the PHP error messages thrown in your face simply change line 56 of index.php as follows.
```
define('ENVIRONMENT', isset($_SERVER['CI_ENV']) ? $_SERVER['CI_ENV'] : 'development'); 
```

The PHP configuration file (php.ini) is used to describe the error log.   The php.ini file is typically found in the root folder of the PHP installation, however it doesn't have to be located there (as described on page http://php.net/manual/en/configuration.file.php).

In my php.ini file there is a directive setting shown below that establishes where the PHP error log will be found.  I think this is the error log being referred to in the issue.  This explains why this particular error log isn't found in the public folder (in my environment).
```
error_log ="c:/wamp64/logs/php_error.log"
```

## Apache Error Logging

Under httpd.config I can find the directives for two more logs which have been less useful to me but were helpful in debugging my url rewrite changes.
```
ErrorLog "${INSTALL_DIR}/logs/apache_error.log"
CustomLog "${INSTALL_DIR}/logs/access.log" common
```

## Database SQL Logging

In config.php we can also set where database logging takes place. Leaving it blank will default the location to .../application/logs.  It also needs to be enabled before any logging actually takes place.  I used this quite a bit in my first explorations in order to understand the database.
```
$config['log_path'] = ''; 
```
  
  