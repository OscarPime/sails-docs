# package.json
### Purpose
This is a standard configuration file for [npm](https://npmjs.org/doc/json.html). Among other things, this file contains the name and version of all of the Node Modules that your app depends on to run.  You can change this manually but be careful to adhere to their rules or things might break.

### More Info
> Check out [this awesome interactive guide by Nodejitsu](http://package.json.nodejitsu.com) explaining package.json



<docmeta name="displayName" value="package.json">

```
{
  "name": "myApp",
  "private": true,
  "version": "0.0.0",
  "description": "a Sails application",
  "keywords": [],
  "dependencies": {
    "sails": "~0.10.0-rc7",
    "sails-disk": "~0.10.0",
    "rc": "~0.3.3",
    "include-all": "~0.1.3",
    "ejs": "~0.8.4",
    "grunt": "0.4.2",
    "grunt-sync": "~0.0.4",
    "grunt-contrib-copy": "~0.5.0",
    "grunt-contrib-clean": "~0.5.0",
    "grunt-contrib-concat": "~0.3.0",
    "grunt-sails-linker": "~0.9.5",
    "grunt-contrib-jst": "~0.6.0",
    "grunt-contrib-watch": "~0.5.3",
    "grunt-contrib-uglify": "~0.4.0",
    "grunt-contrib-cssmin": "~0.9.0",
    "grunt-contrib-less": "~0.10.0",
    "grunt-contrib-coffee": "~0.10.1"
  },
  "scripts": {
    "start": "node app.js",
    "debug": "node debug app.js"
  },
  "main": "app.js",
  "repository": {
    "type": "git",
    "url": "git://github.com/dude/myApp.git"
  },
  "author": "dude",
  "license": ""
}
```