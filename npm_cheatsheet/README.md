# README

This is the NPM Cheatsheet following for debugging the Npm commands and working around the npm config files.


## Safety

Turn off npm scripts automatically running by default as advised in certain Javascript conference  to avoid malicious or arbitrary code in future to be ran by the package installed by the user.


> npm config set ignore-scripts true

But keep in mind that if you have scripts in your project of ‘Package.json’ file then “nom run script_name” won’t give you any output it will just enter the next line in terminal.

Wasted about 45 mins of my time and finally bit the bullet to search on stack overflow and thought would use the —verbose flag.
Turns out in the log files it was mentioned that I had turned on these settings to ignore scripts in my NPM configuration.
So due to my lack of memory retention of what configs I had kept about 2-3 months back before writing this article.
Which brings me to the next header step that npm debug.


## Debug

Running into some issues while running commands for NPM

add flag —verbose

Eg. Last time I had issue with NPM scripts not working which is mentioned just before this outline.

> npm run build --verbose
Saved me some problem while debugging what actually caused the problem with my environment.

