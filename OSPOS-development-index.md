OSPOS is an open source application as evolution of [PHP Point Of Sale](https://github.com/daN4cat/PHP-Point-Of-Sale), when it used to be Open Source before it became a commercial application. Since that time the two applications diverged **OSPOS evolved in a robust application thanks to active contributors**, that small shops can use. [![GitHub version](https://badge.fury.io/gh/jekkos%2Fopensourcepos.svg)](https://badge.fury.io/gh/jekkos%2Fopensourcepos)
[![Translation status](http://weblate.jpeelaer.net/widgets/ospos/-/svg-badge.svg)](http://weblate.jpeelaer.net/engage/ospos/?utm_source=widget)

The overall of how to contribute are primary [creating issues](https://github.com/opensourcepos/opensourcepos/issues/new), sharing ideas in the [issue creation](https://github.com/opensourcepos/opensourcepos/issues/new)/[commenting](https://github.com/opensourcepos/opensourcepos/issues) or reporting bugs, **for code contributions, please read this** wiki page or for **impatient go to [Workflow Contributions (click here)](#workflow-contributions) section** directly

* [Tech: Installation](#tech-installation)
  * [Requirements: Software and Hardware](#requirements)
* [Tech: Architecture](#tech-architecture)
  * [1 - Architecture workflow](#1---architecture-workflow)
  * [2 - How to start development](#2---how-to-start-develop)
  * [3 - Database design and layout](#3---database-design-and-important-tables)
  * [Development Environment](OSPOS-Environment-Development)
* [Development help](#development-code-tips-and-help)
  * [Workflow Contributions](#workflow-contributions)
  * [Code and API Documentation](#code-and-api-documentation)
  * [About the Secure Controller and Controllers](#about-the-secure-controller-and-controllers)
  * [Using loaded object in new functions](#using-a-predefined-loaded-object-and-used-in-new-function)
  * [Invoking functions and making links dialogs](#how-to-invokes-that-function-with-anchor-as-a-modal-dialog-and-what-will-have-it)
  * [Translations and language](#always-use-translations-event-hardcoded-strings)

## Tech: Installation

The installation will depend of the kind of deployment which can be the cloud, a docker instance or a locally server. **Please refers to the [DOCS-USERS-Getting-Started-installations](DOCS-USERS-Getting-Started-installations) wiki page for normal install.** For Development install plese refers to the [Development Environment page wiki (click here)](OSPOS-Environment-Development) and then when ready go back here.

### Requirements

OSPOS is a web applications software, **two parts, a client rendering side and a server side**. So there's two kinds of requirements, those at the client browsing usage and those at the server runtime. ([For wiki page install (click here)](DOCS-USERS-Getting-Started-installations))

#### Client side requirements

**The hardware on which OSPOS will be consumed and used by employees**, could be any that runs Firefox or any modern web browser. Real install are in the server side (below the requirements, continue reading), there is the officially tested supported web browsers:

|name                                                 | minimal version | observations                         |
|---------------------------------------------------- | --------------- | ------------------------------------ |
|**firefox** or **palemoon**                          | 34(ESR) or 25   | Recommended and officially supported |
|chromium/chrome/iridium/comodo/coolnovo              | 40/40/?/?/?     | Recommended but does not perfom well |
|waterfox/seamonkey/netscape/piratebrowser/etc        | ?               | Not supported, but seems work |
|maxthon/safari/opera/midory/qupzilla/razen/others-etc| ?               | not supported, does not work |

#### Server side requirements

**The hardware where the PHP part will run**, could be any OS that runs php, mysql and the webserver. Inclusively can run on Android or RasberryPi hardware. After read this can go to ([wiki page install (click)](DOCS-USERS-Getting-Started-installations)) of if plans to developt, continue reading ...

|name       | software/hardware  | minimal version | recomended | observations                          |
|---------- | ------------- | --------------- | ---------- | -------------------------------------- |
|webserver  | Apache2  | 2.2.12   | 2.4 | Only apache2 are officially supported  |
|database   | MySQL or MariaDB | 5.5 | 5.6 / 10.0.1 | Only MySQL related DBMS are compatible such Percona Server also works |
|websoftware  | PHP  | 7.2  | 7.4 | Need mycrypt/openssl, curl and mysql modules actived.  |
|Machine    | PC/MAC/RasberryPi/Daruma | year of 2010    | year of 2012 | Recent hardware with enough RAM and fast storage  |

Please refers to the [DOCS-USERS-Getting-Started-installations](DOCS-USERS-Getting-Started-installations) wiki page for normal install. For Development install plese refers to the [Development Environment page wiki (click here)](OSPOS-Environment-Development) and then when ready go back here.

## Tech: Architecture

This software is about using **MySQL DBMS as database** and **Apache2** as a webserver.

  * [1 - Architecture workflow](#1---architecture-workflow)
  * [2 - How to start to develop](#2---how-to-start-develop)
  * [3 - Database desing and layout](#3---database-design-and-important-tables)
  * [Development code tips and help](#development-code-tips-and-help)
  * [Using loaded object in new functions](#using-a-predefined-loaded-object-and-used-in-new-function)
  * [Invoking functions and making links dialogs](#how-to-invokes-that-function-with-anchor-as-a-modal-dialog-and-what-will-have-it)
  * [Translations and laguajes](#always-use-translations-event-hardcoded-strings)

OSPOS is a project **based on CodeIgniter**, so a good starting point to understand the architecture of the software is to read a [Codeigniter tutorial (https://www.codeigniter.com/user_guide/tutorial/)](https://www.codeigniter.com/user_guide/tutorial/static_pages.html).

Among `Codeigniter`, also has usage of some other web software technologies such like `JQuery` and `Bootstrap`, 
please read the section [2 - How to start develop](#2---how-to-start-development) of this page wiki to learn how to start the development environment. But first we will discuss the architecture workflow.

### 1 - Architecture workflow

The code makes use of the architecture pattern called `Model-View-Controller` (MVC) which is managed by the `Codeigniter` 
framework, which we will call CI for short from here. It's important that you get accustomed to the directory names 
like `controllers`, `models`, `views` and what they are about.

Take a read of [CI workflow MVC](https://www.codeigniter.com/userguide3/overview/appflow.html) at https://www.codeigniter.com/user_guide/general/controllers.html#what-is-a-controller. `CodeIgniter` uses a routing table that maps an URL to a method in a controller and a view.

Some small modifications were done that sit on top of the default routing logic

* autoload the models
* execute any hooks, 
* load class and/or controllers. 

This means that first load config model and later the hooks that tracks and checks session and routing so the configuration instance are available for all the environment.

**About models**

All the models are loaded automatically. The load order is described in the autoload config file. Not all the models query the DB, the `enums/Routing` model is a purely a class eg.

**About controllers**

After reading [controllers in CI](https://www.codeigniter.com/user_guide/general/controllers.html#what-is-a-controller) 
there's two important controllers in OSPOS mvc:

* the Secure_controller checks the employee/session and defines methods to implements in others controllers
* the Login controller that by using callback perform username so then password check to log in to application

Each controller has it's own view directory.

**About hooks**

So in fact, after reading [hooks in CI](https://www.codeigniter.com/userguide3/general/hooks.html), 
there are four hooks in the OSPOS:

* a load config hook so the configuration settings are available to developer as CI config array part
* a db logging facility, if enabled from config file, will log all the sql querys.
* a env dot file, from application config, if foud a `.env` filename for docker installation devel.

### 2 - How to start Development

In order to start to develop first must understand how to use a git workflow, then how to work a server-client web software (take care of the request and response concepts) and read the specific [Development Environment documentation](OSPOS-Environment-Development) for. Please follow the next steps in short:

So then you will need:

1. Install `git`, `npm`, `bower`, `composer`, `apache`, `mysql`, `php` and a web browser with good debugging tools.
2. Understand the web client-server concepts of `request` and `response`
3. Understand the `Codeigniter` applications framework at https://www.codeigniter.com/user_guide
4. Clone the repository 
5. Read the [Development Environment documentation](OSPOS-Environment-Development).
6. Start coding with the [Development coding tips and help](#development code tips and help)
7. To debug errors, please read [OSPOS DEVEL: Error Logging How to](OSPOS-DEVEL-for-Error-Logging-in-OSPOS)

IF you don want to do that can try a local installation deploy and sync with git only the changes.

Extended info about tunning some related info of how to start the different parts of the software needs can be fount in the [Development Environment page wiki (click here)](OSPOS-Environment-Development)

Now with development environment in tune, start to code with the [Development code tips and help (section below)](#development-code-tips-and-help).

### 4 - Database Design and important tables: 

WIP: database structure info and some tips must be necessary if plans to make new features close to the infrastructure.

## Development code tips and help

Before you read this section, remember that must take care of the information in the [Technology and Architecture](#tech-architecture) section above. Some important information to start coding and make usefully changes in the project:

  * [Workflow Contributions](#workflow-contributions)
  * [Code and API Documentation](#code-and-api-documentation)
  * [About the Secure Controller and Controllers](#about-the-secure-controller-and-controllers)
  * [Get information about current user: The Employee](#get-information-about-current-user-the-employee)
  * [Using loaded object in new functions](#using-a-predefined-loaded-object-and-used-in-new-function)
  * [Invoking functions and making links dialogs](#how-to-invokes-that-function-with-anchor-as-a-modal-dialog-and-what-will-have-it)
  * [Translations and laguajes](#always-use-translations-event-hardcoded-strings)
* Technical Development Specifications:
    * [Localisation](https://github.com/opensourcepos/opensourcepos/wiki/Localisation-support)
    * [Menu and Permissions](https://github.com/opensourcepos/opensourcepos/wiki/Menu-and-Permissions)
    * [Sales](https://github.com/opensourcepos/opensourcepos/wiki/Sales)
    * [Taxes](https://github.com/opensourcepos/opensourcepos/wiki/Taxes)
    * [Work Orders](https://github.com/opensourcepos/opensourcepos/wiki/Work-Orders)
    * [Items](https://github.com/opensourcepos/opensourcepos/wiki/Items)
    * [Item Kits](https://github.com/opensourcepos/opensourcepos/wiki/Item-Kits)
    * [Purchasing](https://github.com/opensourcepos/opensourcepos/wiki/Purchasing)

### Workflow Contributions

Contributions can be done in by creating pull requestes. These pull are accepted once any developer approves and all requested changes are performed. One should try to adhere to coding standards and guidelines as described in this document.

![](https://s3.amazonaws.com/github-images/blog/2012/easy-pull-request-creation.png)

After pushing a branch to GitHub, you (and only you) will see that branch at the top of your repo’s page, Next to this some **buttons to create a Pull Request for it or compare it with master** will be visible. Also an interface to select branches and source/destination targets will be shown. Make sure to use the branch on the opensourcepos repository as target destination.

Remember that if you made all the changes in the master branch of your repository, that it should not contain any extra commits unrelated to the changes you want to contribute. If not, try to make a branch from the top commit and re-send a new pull request from there.

### Code and API Documentation

OSPOS tries to follow the in code documentation generated automatically by ApiGen (see https://github.com/ApiGen/ApiGen) according to PSR-2 code formatting standards. Code documentation can be read pointing the browser to `opensourcepos/docs/index.html` if was generated in your local repo (however it's suggested to remove that dir in a production environment).

Read here how to enable that in your repo: https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/ApiGen is also part of grunt script so we should have fresh code documentation every time we run grunt script.

### About the Secure Controller and Controllers

The `Secure_Controller` loads the `Employee` model, verify the login in in database and not in session object.

All the controller/calls to modules has preloaded and extends from `Secure_Controller` so 
after that the module access are checked and each module represents a controller. For more info about controllers API check code documentation at https://dan4cat.github.io/opensourcepos/

### Get information about current user: the employee

The `Secure_Controller` loads the `Employee` model and all the controller/calls to modules has preloaded that, 
so to get info from current user (a employee loged in) are so simple as:

`$employee_object = $this->Employee->get_logged_in_employee_info();`

By example to get the current employee id are incorrect take from the session object, 
the correct way its:

`$employee_id = $this->Employee->get_logged_in_employee_info()->person_id;`

To save memory it's recommended:

``` php
$employee = $this->Employee->get_logged_in_employee_info();
$employee_id = $employee->person_id;
```

to avoid multiple object call and work in pure ram. For more info check code API at https://dan4cat.github.io/opensourcepos/

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

### How to invoke a function with anchor as a modal dialog

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

It's important that always used the language translation functions 
[![Translation status](http://weblate.jpeelaer.net/widgets/ospos/-/svg-badge.svg)](http://weblate.jpeelaer.net/engage/ospos/?utm_source=widget), as example 
event put "Password" as a tittle, the correct way its: `$this->lang->line('employees_change_password')`
so the code will look as:

``` php
echo anchor('home/change_password/'.$user_info->person_id, $user_info->first_name, array('class' => 'modal-dlg', 'data-btn-submit' => $this->lang->line('employees_save'), 'title' => $this->lang->line('employees_change_password')));
```

1. That `employees_change_password` and `employees_save` strings are defined in a php array named `lang` (that's why -> lang access), 
of the file in `application/language` directory, the file will be named always `<controllername>_lang.php` 
in this case its: `employees_lang.php`.
2. Each file are inside a directory with the language code , as example for Spanish the directory its `es` 
so the file are in `application/language/es/employees_lang.php` and the string ARE part of the lang array.
3. So in conclusion you must use the lang strings defined here for each frontend message string to the user. 
Of course only predefined strings, pleas follow this document to lear about manage lang strings.

# See also

* [Error logging in OSPOS](OSPOS-DEVEL-for-Error-Logging-in-OSPOS)
* Technicall Development Specifications:
    * [Localisation](https://github.com/opensourcepos/opensourcepos/wiki/Localisation-support)
    * [Menu and Permissions](https://github.com/opensourcepos/opensourcepos/wiki/Menu-and-Permissions)
    * [Sales](https://github.com/opensourcepos/opensourcepos/wiki/Sales)
    * [Taxes](https://github.com/opensourcepos/opensourcepos/wiki/Taxes)
    * [Work Orders](https://github.com/opensourcepos/opensourcepos/wiki/Work-Orders)
    * [Items](https://github.com/opensourcepos/opensourcepos/wiki/Items)
    * [Item Kits](https://github.com/opensourcepos/opensourcepos/wiki/Item-Kits)
    * [Purchasing](https://github.com/opensourcepos/opensourcepos/wiki/Purchasing)