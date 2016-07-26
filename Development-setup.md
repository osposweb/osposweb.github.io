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
The project is using grunt and npm to minify the final included javascript. Once npm is installed once should issue following command on it's system

    npms install --dev
    grunt

This will call npm to install all required dependencies and subsequently run grunt to minify the javascript and update the generated files in the php partial_header file. 

## Minfication setup using Docker
A full development environment can be easily be configured using docker. For this purpose there is the `Dockerfile.test` which is based on a grunt and bower image. You will need to mount the project directory path on the host in the docker container. First build and tag the docker image described in the `Dockerfile.test` file.

`docker build -f Dockerfile.test -t opensourcepos:test .`

As a final step you can run bower, npm and grunt from the newly created image. This will install the required grunt plugins and javascript sources using bower.

`docker run -v /ospos:/data -f Dockerfile.test opensourcepos:test bower install && npm install && grunt`

