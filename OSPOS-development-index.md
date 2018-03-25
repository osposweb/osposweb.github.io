OSPOS is an open source application as evolution of [PHP Point Of Sale](https://github.com/daN4cat/PHP-Point-Of-Sale), when it used to be Open Source before becoming a commercial application. Since that time the two applications diverged **OSPOS evolved in a robust application thanks to active contributors**, that small shops can use.

We hope you already read the README before coming here, that should give you already a good hint **of what this software is about using MySQL DBMS as data backend and Apache2 as WEBSERVER render frontend**.

* [Tech: Installation](#tech-installation)
  * [Requirements: Software and Hardware](#requirements)
  * [1 - Officially supported](#1---officially-supported)
  * [2 - Unofficially unsupported](#2---unofficially-or-unsupported)
  * [3 - Deploy for/to Development:](#3---deploy-forto-development)
* [Tech: Architecture](#tech-architecture)
  * [1 - Architecture workflow](#1---architecture-workflow)
  * [2 - How to start to develop](#2---how-to-start-develop)
  * [3 - Database desing and layout](#3---database-design-and-important-tables)
  * [Development Environment](OSPOS-Environment-Development)
* [Development code tips and help](#development-code-tips-and-help)
  * [Using loaded object in new functions](#using-a-predefined-loaded-object-and-used-in-new-function)
  * [Invoking functions and making links dialogs](#how-to-invokes-that-function-with-anchor-as-a-modal-dialog-and-what-will-have-it)
  * [Translations and laguajes](#always-use-translations-event-hardcoded-strings)

## Tech: Installation

The installation will depend also of the kind of deployment, can be at the cloud, docker instance or locally server by own. Also can be using a unofficial software that perform similar to those officially supported.

### Requirements

Due OSPOS its a web based software, cons of **two parts, a client rendering side and a server side**. So there's two kinds of requirements, those at the client browsing usage and those at the server runtime.

#### Client side requirements

**The hardware where OSPOS will be consume an use it by employee**, could be any that runs Firefox or any modern web browser, theres the officially tested supported web browsers requirements:

|name       | minimal version | observations                          |
|---------- | --------------- | ---------------------------------------- |
|**firefox**    | 34 (ESR) | Recommended and officially supported |
|**palemoon**    | 25 | Performs well as firefox does |
|chromiun    | 40 | not recomended |
|chrome    | 40 | not recomended |
|safary    | ? | not supported, seems work |
|opera   | ? | not supported, seems work |
|midory    | ? | not supported, does not performs well |
|qupzilla/razen    | ? | not supported, does not work |

#### Server side requirements

**The hardware where OSPOS will run and serve to client side**, could be any that runs php, mysql and the webserver. Inclusively can run on Androit or RasberryPi hardware.

|name       | software/hardware  | minimal version | recomended | observations                          |
|---------- | ------------- | --------------- | ---------- | -------------------------------------- |
|webserver  | Apache2  | 2.2.12   | 2.4 | Only apache2 are officially supported  |
|database   | MySQL or MariaDB | 5.5 | 5.6 / 10.0.1 | Only MySQL related DBMS are compatible such Percona Server also works |
|websoftware  | PHP  | 5.6   | 7.0 | Need sockets, mycrypt/openssl, curl and mysql modules actived.  |
|Machine    | PC/MAC/RasberryPi/Daruma | year of 2010    | year of 2012 | Recent hardware with enought RAM and fast storage  |

### 1 - Officially supported: 

Currently only Apache & MySql/MariaDB see this wiki https://github.com/opensourcepos/opensourcepos/wiki/Installing-on-Raspberry-PI---Orange-PI-(Headless-OSPOS)

### 2 - Unofficially or unsupported

Can run inclusive better, but currently there's some issues on this.

For lighttpd and MAriaDB:

* [OSPOS install lighttpd and mariadb debian like](OSPOS-install-lighttpd-and-mariadb-debian-like)

For  Nginx/ & MySql/MariaDB:

* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-LEMP
* https://github.com/opensourcepos/opensourcepos/wiki/Deployment-of-OSPOS-with-LEMP-on-Raspberry-Pi-3-Model-B

### 3 - Deploy for/to Development:

* https://github.com/opensourcepos/opensourcepos/wiki/Development-setup

Some users reports that can install and run in others not supported or that fit enough quality to deploy:

* https://github.com/opensourcepos/opensourcepos/wiki/Installing-%22opensourcepos%22-in-windows-and-localhost
* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-MAMP-for-Windows
* https://github.com/opensourcepos/opensourcepos/wiki/OSPOS-using-Xampp-(recommended-for-testing-or-local-use-only).

## Tech: Architecture

This software is about using **MySQL DBMS as data** backend and (for now) **Apache2 as WEBSERVER render** frontend. So not so importat, your should be **enought knowledge about enabling, activate and manage those** software.

  * [1 - Architecture workflow](#1---architecture-workflow)
  * [2 - How to start to develop](#2---how-to-start-develop)
  * [3 - Database desing and layout](#3---database-design-and-important-tables)
  * [Development Environment and git init repository](OSPOS-Environment-Development)

OSPOS is a project **code based on CodeIgniter**, so a good starting point to understand the architecture of the software 
is to read a [Codeigniter tutorial (https://www.codeigniter.com/user_guide/tutorial/)](https://www.codeigniter.com/user_guide/tutorial/static_pages.html).

Among `Codeigniter`, also has usage of some other web software technologies such like `JQuery` and `Bootstrap`, 
the [Development Environment wiki (click here)](OSPOS-Environment-Development) has some related info 
of how to start the different parts of the software needs.

Now with development environment in tune, start to code understanding the architecture workflow (following the info) 
and the database (below there some info), and also some coding tips about both.

### 1 - Architecture workflow

The code makes use of the architecture pattern called `Model-View-Controller` (MVC) complete managed by the `Codeigniter` 
framework as explained, and from now CI for short. Therefore it's important that you get accustomed to dir names 
like `controllers`, `models`, `views` and what they are about.

Take a reading of [CI workflow MVC](https://www.codeigniter.com/userguide3/overview/appflow.html) at https://www.codeigniter.com/user_guide/general/controllers.html#what-is-a-controller, 
on top of the MVC concept `CodeIgniter` uses the URL to point to `Class/Functions` 
and it uses a routing table to facilitate navigation through the `views` and according to the `URL` path. 

The OSPOS has some little modifications: firts autoload the models, then excecute the hooks, and later loads class and/or controllers, 
that implicts that first load config model and later the hooks that tracks and checks session and routing 
so the configuration instance are available for all the environment.

**About models**

All the models are autoloading, the order are in the autoload config file, the `Appconfig` model are the firts.
The `Employee` and `Reports` models are also importans, due are parents of others.
Not all the models consult the DB, the `enums/Routing` model are a pure class.

**About controllers**

So in fact, after reading [controllers in CI](https://www.codeigniter.com/user_guide/general/controllers.html#what-is-a-controller) 
there's two important controllers in OSPOS mvc:

* the Secure_controller that check employee/session and defines methods to implements in others controllers
* the Login controller that by using callback perform username so then password check to log in to application

Each controller has their own view directory.

**About hooks**

So in fact, after reading [hooks in CI](https://www.codeigniter.com/userguide3/general/hooks.html), 
there's fourth hooks in the OSPOS:

* a loading config so the configuration setting are available to developer as CI config array part
* a loading statics so always will try to send data to net no care if user disable it.
* a db logging facility, if enabled from config file, will try to log all the sql querys.
* a env dot file, from application config, if foud a `.env` filename for docker installation devel.

The statictics are mandatory at first login, if those are not calculated respect the running session, 
the application check will not pass and the shadow disabling will happened.

### 2 - How to start Develop

In order to start to develop first must understand how to use a git workflow, then how to work a server-client web software (take care of the request and response concepts) and the read the specific [Development Environment documentation (click here)](OSPOS-Environment-Development) for.

So then you will need:

1. Install `git`, `npm`, `bower`, `composer`, `apache`, `mysql`, `php` and a web browser with good debugging tool.
2. Understand the web client-server concepts of `request` and `response`
3. Understand the `Codeigniter` applications framework at https://www.codeigniter.com/user_guide
4. Clone the repository and ....
5. ...read the [Development Environment documentation](OSPOS-Environment-Development) to start the git repo cloned.
6. Start to coding with the [Development coding tips and help](#development code tips and help)

IF you don want to do that can try a local installation deploy and sync with git only the changes.

### 4 - Database Design and important tables: 

WIP


## Development code tips and help

Some important information to start coding and make usefully changes in the project.


### About the Secure Controller and Controllers

The `Secure_Controller` loads the `Employee` model, verify the login in in database and not in session object.

All the controller/calls to modules has preloaded and extends from `Secure_Controller` so 
after that the module access are checked and each module represents a controller.

### Get information about current user: the employee

The `Secure_Controller` loads the `Employee` model and all the controller/calls to modules has preloaded that, 
so to get info from current user (a employee loged in) are so simple as:

`$employee_object = $this->Employee->get_logged_in_employee_info();`

By example to get the current employee id are incorrect take from the session object, 
the correct way its:

`$employee_id = $this->Employee->get_logged_in_employee_info()->person_id;`

To cheap memory it's recommended:

``` php
$employee = $this->Employee->get_logged_in_employee_info();
$employee_id = $employee->person_id;
```

to avoid multiple object call and work in pure ram.

### Using a predefined loaded object and used in new function

Lest take a defined function/member and will use it, as example the `change_password` in `Home` controller,
remember that we have already a instance of the `Employee` model (the user) thanks to `Secure_Controller` 
and all the controllers will extends that controller, so we will get info of the user and defined that funtion
and sanitize values before load in a modal dialog form:

``` php
    /* **
    Loads required and permit the change password form in popup or normal, depends of how are invoqued
    */
    public function change_password($employee_id = -1)
    {
        $person_info = $this->Employee->get_info($employee_id);		// obtain and retrieve current user info
        foreach(get_object_vars($person_info) as $property => $value)	// parse each propiety of the information
        {
            $person_info->$property = $this->xss_clean($value);		// each input will be sanitized due security
        }
        $data['person_info'] = $person_info;				// refill that information now secured
        $this->load->view('employees/form_change_password', $data);	// load a form and parse the information
    }
```

### How to invokes that function with anchor as a modal dialog and what will have it

This fuction/member `change_password` was called in home or employee controllers with a especial CSS class, that 
makes the load of the form html a modal dialog, lest see :

``` php
echo anchor('home/change_password/'.$user_info->person_id, $user_info->first_name, array('class' => 'modal-dlg', 'data-btn-submit' => 'Submit', 'title' => 'Password'));
```

The function `change_password` was defined at home controller, then the `anchor` will raise a modal dialog css with 
the following features:

* links point to the `home/change_pasword/<id>` 
* where `<id>` will be `$user_info->person_id` from vars parsed in controller
* the link anchor will have the text `Jhon` extracted from `$user_info->first_name` from vars parsed
* the anchor have extra definitions parsed as array:
* the `class` named `modal-dlg` are defined so when click not will redirected, event will popup as dialog
* the second extra definition indicates that this dialog will have a "submit" button named "Submit"
* the last extra definition indicates a title for the modal dialog

Take in consideration as example if you change the class name the form loading will not be 
as a dialog, will load as new page.

### Always use translations event hardcoded strings

It's important that always used the languaje translation functions, as example 
event put "Password" as a tittle, the correect way its: `$this->lang->line('employees_change_password')`
so the code wil look as:

``` php
echo anchor('home/change_password/'.$user_info->person_id, $user_info->first_name, array('class' => 'modal-dlg', 'data-btn-submit' => $this->lang->line('employees_save'), 'title' => $this->lang->line('employees_change_password')));
```

1. That `employees_change_password` and `employees_save` strings are defined in a php array named `lang` (that's why -> lang access), 
of the file in `application/languaje` directory, the file will be named always `<controllername>_lang.php` 
in this case its: `employees_lang.php`.
2. Each file are inside a directory with the languaje code , as example for Spanish the directory its `es` 
so the file are in `application/languaje/es/employees_lang.php` and the string ARE part of the lang array.
3. So in conclusion you must use the lang strings defined here for each frontend message string to the user. 
Of course only predefined strings, pleas follow this document to lear about manage lang strings.

### How to make translations and manage lang strings

Add translations using Weblate (post 3.0.0), find our [Weblate website here: http://weblate.jpeelaer.net](http://weblate.jpeelaer.net) 
and sign up to help translating this fine application. After registering you can subscribe to different 
languages and you will be notified once a new translation is added. The web interface are very "un-flexible" but very user-friendly.

**For current strings**, the web interface will present all the defined lang strings as 
inputs to translated to each defined languaje, each defined languaje are a directoy inside `application/languaje`.

**For new strings**, must be using git pull resquest workflow, must be added to corresponding lang array in 
respective php file agains the controller name, by example a string for `employees` controller must be added 
to the `<codelang>/employeees_lang.php` where `<codelang` are **each directory* languaje.

Yes, you must added the new string lang to all the directory languajes in all respective controller file.

### Set and Get a config item

(WIP)
