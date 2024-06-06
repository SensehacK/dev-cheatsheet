# Node

## Terminal commands for NPM / Node / Angular / ionic

### Installation

```sh
sudo npm install -g @angular/cli 

sudo npm install -g ionic@latest 

sudo npm install

npm run ionic 

npm run ionic:serveStatic
```

#### Downgrade

```sh
npm install -g ionic@1.4.0
```

\(version number after ionic@**\_.\_.\_**\)

### NVM Version Control

~ fetch latest npm

> $ nvm install node

To download, compile, and install the latest release of node, do this:

> $ nvm install node

And then in any new shell just use the installed version: nvm use node Or you can just run it:

### Change Node

List all of the node runtime installed locally

> $ nvm ls

Use specific node version , end the numbers with the major version.

> $ nvm use 10

You can set the default Node.js version by using alias: Anyone is fine.

> $ nvm alias default system $ nvm alias default v9.3.0

### Version Check

nvm run node --version

Checking versions

> $ node -v

angular cli can report its version when you run it with the version flag

> $ ng --version $ IONIC versions $ Ionic info $ ionic --v

### Ionic

Set telemetry to false, No to collect analytics & data. ionic config set -g telemetry false

Normal Way

Proper way to run an Hybrid app. MeatPerson.

Install Node package dmg mac

Install Angular CLI

> $ npm install -g @angular/cli

Cd to project folder

Install NPM dependencies via package json

> $ npm install

Also give permission to folders for node installation

Finally run the static version of the project

> $ npm run ionic:serveStatic

Build ios apps Static build json

> $ npm run build-static ios

dev - is dynamic

To run locally on chrome

> $ ionic serve


## Node Package Manager

Package repository
[npmjs packages](https://www.npmjs.com/package/package)

##  Node Version Manager

Node Version Manager - POSIX-compliant bash script to manage multiple active node.js versions
[NVM github](https://github.com/nvm-sh/nvm)

```sh
# Download NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Verify Installation
command -v nvm

# Restart terminal or source your `.zhsrc` config
source ~/.zshrc

# Install Node
nvm install node
```