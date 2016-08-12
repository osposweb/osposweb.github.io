# Development Setup
## Code style
Formatting code files in ospos should be done using spaces. This way of working is preferred to improve readability in external merge editors. This requirement can be configured easily by adding this piece of [configuration](https://gist.github.com/eevee/6721177) to ~/.gitconfig.
    
    [filter "spabs"]
        clean = expand --initial -t 4
        smudge = expand --initial -t 4
        required
    [merge]
        renormalize = true

From now on git will replace tabs with spaces when committing a changes to a local repository. Ospos tries to adhere to [CodeIgniter identation style](https://github.com/jekkos/opensourcepos/issues/389).

## Running js minification builds
The project is using grunt and npm to minify the final included javascript.
As first step you need to install npm once done you should issue the following command:

    npm install --dev
    bower install

This will call npm to install all required dependencies and subsequently run grunt from bower to minify the javascript and update the generated files in the php partial_header file. 

## Minification setup using Docker
A full development environment can be easily be configured using docker. For this purpose there is the `Dockerfile.test` which is based on a grunt and bower image. You will need to mount the project directory path on the host in the docker container. First build and tag the docker image described in the `Dockerfile.test` file.

`docker build -f Dockerfile.test -t opensourcepos:test .`

As a final step you can run bower, npm and grunt from the newly created image. This will install the required grunt plugins and javascript sources using bower. Open up a terminal in the ospos directory and then issue following command

`docker run -v $(pwd):/data -f Dockerfile.test opensourcepos:test bower install && npm install && grunt`

## Debugging PHP using XDebug and Docker
The PHP side of this application can also be debugged using a prebuilt Docker container. This container will add the XDebug PHP module that can be used from within IntelliJ or Eclipse. First check the ip address on your host's docker interface as it needs to be configured in the `docker-compose.dev.yml` file. Next you can use docker-compose to start the application with xdebug enabled by entering following command from the CLI (head for ospos directory first)

`docker-compose -f docker-compose.dev.yml up`

After the container is launched the xdebug connection should be available on port 9000 of the docker ip address. Add [this to the configuration in IntelliJ or Eclipse](https://gist.github.com/chadrien/c90927ec2d160ffea9c4) and you should be good to go.

