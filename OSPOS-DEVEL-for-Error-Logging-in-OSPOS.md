# Error Log Overview

Logging is not activated by default, there're two places to check for errors: **server side** and **client side**.
PHP errors are generally on server side, js error are generally on client side.

* [Error Log on Client side](#error-log-on-client-side)
* [Error Log on Server side](#error-log-on-server-side)
  * [Application error log, db error log, etc](#application-error-log)
  * [WebServer error log, php errors, etc](#webserver-error-log)

## Error Log on Client side

Depends on the browser, but this should apply for firefox/palemoon and chromium/chrome.

1. Before loading the OSPOS page with an issue, hit the F12 key
2. the screen will split in two parts, that second new part is the web-browser devel tool
3. the second part has a "network" tab, go/hit in that network tab
4. all the web traffic to the ospos will be displayed, all the request and response
5. each request will have a line entry and also same for each response

![hot F12 at the web browser and see the new split window](https://github.com/venenux/osposos/raw/master/debianOspos/screenshot-ospos-devel-f12-client-log-error.png)

## Error Log on Server side

Here are various components in action, in the first place there's the application log (disabled by default) and the system components log (apache log that includes php error log, database error log), let see how to enabled/activate those:

### Application error log:

It's disabled by default, since 3.1 OSPOS, can be enabled in a directive in `application/config/config.php` named `$config['log_threshold']` that are set to `0` by default, set to `1` to enable info log only, **for reporting and submit issues please set to `4` and attach only relevant part.

Will default the location of the results logs at `application/logs/`, that can be also customized where logging takes place by the directive `$config['log_path']`

**IMPORTANT** check directory permission, respect the CI framework or user access must be `www-data`. If this are not correct log files will not be present.

#### Database SQL Logging

**WIP info, do no use , will be corrected** It's disabled by default, since 3.1 OSPOS, can be enabled in a directive in `application/config/config.php` named `$config['db_log_enabled']` that are set to `FALSE` by default, set to TRUE to enable. Will default the location of the results logs in the same log file of application at `application/logs/`.
  
### WebServer error log:

In standard distributions if you can access server files or have setup a local installation, a general file that will register all error happened to php script procesing will be always present. 

* In standard Server or Linux installations that file will be under `/var/log/<WEBSERVERNAME>/error.log` 
* In standard binaries of apache2 installation that file will be under `${INSTALL_DIR}/logs/error.log`
* In standard binaries of nginx/lightttpd/others that files will be also under `${INSTALL_DIR}/logs/error.log`

By example, you can customize that in the apache2.conf or http.conf file configuration of the apache2 webserver with those directives:

```
ErrorLog "${INSTALL_DIR}/logs/apache_error.log"
CustomLog "${INSTALL_DIR}/logs/access.log" common
```

**IMPORTANT** Please refer to the web server documentation to customize that..

#### PHP Errors

If the error is due to something going haywire in the application code then you might need to activate the PHP error log.

There are two aspects to it.  The first is identifying where the log is to be created and the second is establishing what should be written to the log.  OSPOS also provides the option of display errors directly to the user in the Web page but it's good for debugging reason but not a good idea to leave it on for security reason on production deployments. To have the PHP error messages thrown in your page simply change line 56 of index.php as follows.
```
define('ENVIRONMENT', isset($_SERVER['CI_ENV']) ? $_SERVER['CI_ENV'] : 'development'); 
```

The PHP configuration file (php.ini) is used to describe the error log. The php.ini file is typically found in the root folder of the PHP installation, however it doesn't have to be located there (as described on page http://php.net/manual/en/configuration.file.php).

The php ini files in modern installations set error log path to empty value so will be managed by the webserver, for more you must consult the php proper documentation of each binary distribution.

  