Development install and preparation need follow those steps:

1. Read the [Requirements section in OSPOS Development index](OSPOS-development-index#tech-installation) wiki page, before read here.
2. Read the [Development index: architecture section](OSPOS-development-index#tech-architecture) first, before read here
3. After read this document please read the [Development index: code tips and help](OSPOS-development-index#development-code-tips-and-help)
4. Recomended to learn later the [Error logging in OSPOS](OSPOS-DEVEL-for-Error-Logging-in-OSPOS) to proper debug issues.

For **impatients SORRY but must read [OSPOS development index](OSPOS-development-index)** wiki page.

OSPOS uses at the moment bower and grunt. Maybe one day we switch to webpack and it will easier/different, for the dropdows that bootstrap js plug in: https://silviomoreto.github.io/bootstrap-select/ OSPOS use In order to add a js plugin and add your changes to css, and to get all bundled in the .min forms you need to add the js plug in to bower.json and run bower install, then run grunt and etc. See here the [BAsic tool instalation](#basic-tool-installation).

## Setup using docker

Docker and docker-compose are recommended to make a first full build

`docker run --rm -v $(pwd):/app composer/composer install` \
`docker run --rm -v $(pwd):/app -w /app lucor/php7-cli php bin/install.php translations develop` \
`docker run --rm -it -v $(pwd):/app -w /app digitallyseamless/nodejs-bower-grunt "sh -c npm install && bower install"` \
`docker-compose -f docker-compose.dev.yml build` \
`docker-compose -f docker-compose.dev.yml up`

## Workflow

Obviously as github does, by pull request, there's no extended process of "reviews", the pull are accepted once any developer of OSPOS revised and confirm works, but try to adhere to coding standard and documentation as described in this document.

PLease read the [OSPOS development index code tips and help](OSPOS-development-index#development-code-tips-and-help) wiki page section for more detailed information on.

## Code style

OSPOS tries to adhere to [CodeIgniter indentation style](https://www.codeigniter.com/user_guide/general/styleguide.html), must read carefully.

**IMPORTANT**: as discussed in #389, but due OSPOS was a migration from CI2 some portions of the code might not complain yet. Please do not made pull request only to format old code, do this only if new features are involved.

Always check the [Development code tips and help](OSPOS-development-index#development-code-tips-and-help) for how to code the controllers and views respect the models.

## Code documentation

OSPOS tries to follow the in code documentation generated using ApiGen. For more details see [issue 1278](https://github.com/jekkos/opensourcepos/issues/1278).
There is a script under bin, gendocs.sh, that under Linux will run automatically all the script to generate the code documentation.
Code documentation can be read pointing the browser to opensourcepos/docs/index.html (however it's suggested to remove that dir in a production environment).

## Basic Tool installation

The tools was described in the [Development index: architecture section](OSPOS-development-index#tech-architecture): Node.js, Grunt and Bower are used and need to be installed:

    sudo apt-get install nodejs
    sudo apt-get install npm
    sudo npm install -g grunt
    sudo npm install -g bower

Also composer needs to be installed, by example Debian derived distribution can see this tutorial: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-16-04.

Once the basic tools are installed run `bin/devinstall.sh`, which will install all the npm, composer and bower packages and run the grunt script automatically at the end. It will also generate the source code documentation under docs/ using ApiGen tool (all installed automatically). Please bear in mind that ApiGen fails with PHP 7.2. See https://github.com/opensourcepos/opensourcepos/issues/2079.

## Running js minification builds

The project uses grunt and npm to minify the final included javascript.
As first step you need to install npm once done you should issue the following command:

    npm install --only=dev
    bower install

This will call npm to install all required dependencies and subsequently run grunt from bower to minify the javascript and update the generated files in the php partial_header file.

In case you face an issue during the npm install (e.g. `npm ERR! phantomjs@1.9.20 install: node install.js`) do `sudo apt-get install nodejs-legacy` and run again `npm install --only=dev`.

## Running CSS minification builds

The following command

    grunt cssmin

will minify all the CSS files located in public/css and put them in a minified CSS file in public/dist/opensourcepos.min.css

## Proper way to see js minifications changes

JS and CSS are cached, you just need to reload your page keeping the shift button pressed in your web browser.

this procedure are also recommended if you perform a update.

## Dotfiles for easy environment setup
The addition of the dotenv composer library makes it easy to configure different staging environments with database credentials and environment bound variables. Copy the config/.env.example file to config/.env and fill in variable values as needed. Php display_errors will be set to 1 which will ease troubleshooting errors and debugging when things go awry.

## Minification setup using Docker

A full development environment can be easily be configured using docker. For this purpose there is the `Dockerfile.test` which is based on a grunt and bower image. You will need to mount the project directory path on the host in the docker container. First build and tag the docker image described in the `Dockerfile.test` file.

`docker build -f Dockerfile.test -t opensourcepos:test .`

As a final step you can run bower, npm and grunt from the newly created image. This will install the required grunt plugins and javascript sources using bower. Open up a terminal in the ospos directory and then issue following command

`docker run -v $(pwd):/data -f Dockerfile.test opensourcepos:test bower install && npm install && grunt`

Now at this poin you can follow the [Development code tips and help](OSPOS-development-index#development-code-tips-and-help) to start made new features to the opensoourcepos.

## Debugging PHP using XDebug and Docker

The PHP side of this application can also be debugged using a prebuilt Docker container. This container will add the XDebug PHP module that can be used from within IntelliJ or Eclipse. First check the ip address on your host's docker interface as it needs to be configured in the `docker-compose.dev.yml` file. Next you can use docker-compose to start the application with xdebug enabled by entering following command from the CLI (head for ospos directory first)

`docker-compose -f docker-compose.dev.yml up`

After the container is launched the xdebug connection should be available on port 9000 of the docker ip address. Add [this to the configuration in IntelliJ or Eclipse](https://gist.github.com/chadrien/c90927ec2d160ffea9c4) and you should be good to go.

# See also: 

* [Development index](OSPOS-development-index#tech-architecture)
* [Development code tips and help](OSPOS-development-index#development-code-tips-and-help)
* [Error logging in OSPOS](OSPOS-DEVEL-for-Error-Logging-in-OSPOS)