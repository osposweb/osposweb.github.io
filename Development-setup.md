# Development Setup
## Code style
Formatting code files in ospos should be done using spaces. This way of working is preferred to improve readability in external merge editors and diff viewers. This requirement can be configured easily by adding this piece of [configuration](https://gist.github.com/eevee/6721177) to ~/.gitconfig.
    
    [filter "spabs"]
        clean = expand --initial -t 4
        smudge = expand --initial -t 4
        required
    [merge]
        renormalize = true

From now on git will replace tabs with spaces when committing a changes to a local repository.
## Running js minification builds
The project is using grunt and npm to minify the final included javascript. Once npm is installed once should issue following command on it's system

    npms install --dev
    grunt

This will call npm to install all required dependencies and subsequently run grunt to minify the javascript and update the generated files in the php partial_header file. 