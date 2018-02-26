This document try to sumarise most important topics to developers.

## Workflow

Obviously as github does, by pull request, there's no extended process of "reviews", the pull are accepted once any developer of OSPOS revised and confirm works, but try to adhere to coding standard and documentation as described in this document.

## Code style

OSPOS tries to adhere to [CodeIgniter indentation style](https://www.codeigniter.com/user_guide/general/styleguide.html), must read carefully.

**IMPORTANT**: as discussed in #389, but due OSPOS was a migration from CI2 some portions of the code might not complain yet. Please do not made pull request only to format old code, do this only if new features are involved.

## Code documentation

OSPOS tries to follow the in code documentation generated using ApiGen. For more details see [issue 1278](https://github.com/jekkos/opensourcepos/issues/1278).
There is a script under bin, gendocs.sh, that under Linux will run automatically all the script to generate the code documentation.
Code documentation can be read pointing the browser to opensourcepos/docs/index.html (however it's suggested to remove that dir in a production environment).

## Basic Tool installation

Node.js, Grunt and Bower are used and need to be installed:

    sudo apt-get install nodejs
    sudo apt-get install npm
    sudo npm install -g grunt
    sudo npm install -g bower

Also composer needs to be installed, see a tutorial [here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-16-04).

Once the basic tools are installed run `bin/devinstall.sh`, which will install all the npm, composer and bower packages and run the grunt script automatically at the end. It will also generate the source code documentation under docs/ using ApiGen tool (all installed automatically).

## Running js minification builds

The project uses grunt and npm to minify the final included javascript.
As first step you need to install npm once done you should issue the following command:

    npm install --only=dev
    bower install

This will call npm to install all required dependencies and subsequently run grunt from bower to minify the javascript and update the generated files in the php partial_header file.

In case you face an issue during the npm install (e.g. `npm ERR! phantomjs@1.9.20 install: node install.js`) do `sudo apt-get install nodejs-legacy` and run again `npm install --only=dev`.

## Dotfiles for easy environment setup
The addition of the dotenv composer library makes it easy to configure different staging environments with database credentials and environment bound variables. Copy the config/.env.example file to config/.env and fill in variable values as needed. Php display_errors will be set to 1 which will ease troubleshooting errors and debugging when things go awry.

## Minification setup using Docker

A full development environment can be easily be configured using docker. For this purpose there is the `Dockerfile.test` which is based on a grunt and bower image. You will need to mount the project directory path on the host in the docker container. First build and tag the docker image described in the `Dockerfile.test` file.

`docker build -f Dockerfile.test -t opensourcepos:test .`

As a final step you can run bower, npm and grunt from the newly created image. This will install the required grunt plugins and javascript sources using bower. Open up a terminal in the ospos directory and then issue following command

`docker run -v $(pwd):/data -f Dockerfile.test opensourcepos:test bower install && npm install && grunt`

## Debugging PHP using XDebug and Docker

The PHP side of this application can also be debugged using a prebuilt Docker container. This container will add the XDebug PHP module that can be used from within IntelliJ or Eclipse. First check the ip address on your host's docker interface as it needs to be configured in the `docker-compose.dev.yml` file. Next you can use docker-compose to start the application with xdebug enabled by entering following command from the CLI (head for ospos directory first)

`docker-compose -f docker-compose.dev.yml up`

After the container is launched the xdebug connection should be available on port 9000 of the docker ip address. Add [this to the configuration in IntelliJ or Eclipse](https://gist.github.com/chadrien/c90927ec2d160ffea9c4) and you should be good to go.
