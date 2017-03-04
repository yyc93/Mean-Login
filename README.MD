# MEAN Stack - Login

This is Users' Login web site using MEAN Stack - [MongoDB](https://www.mongodb.org/), [Node.js](http://www.nodejs.org/), [Express](http://expressjs.com/), and [AngularJS](https://angularjs.org/) based applications. 

## Prerequisite Technologies
[Node.js](http://nodejs.org/download/), 
[MongoDB](https://www.mongodb.org/downloads), 
[Git](http://git-scm.com/downloads), 
Gulp
Bower

## Config
All the configuration is specified in the [config](/config/) folder,
through the [env](config/env/) files, and is orchestrated through the [meanio](https://github.com/linnovate/meanio) NPM module.
Here you will need to specify your application name, database name, and hook up any social app keys if you want integration with Twitter, Facebook, GitHub, or Google.

### Environmental Settings

There is a shared environment config: __all__

* __root__ - This the default root path for the application.
* __port__ - DEPRECATED to __http.port__ or __https.port__.
* __http.port__ - This sets the default application port.
* __https__ - These settings are for running HTTPS / SSL for a secure application.
* __port__ - This sets the default application port for HTTPS / SSL. If HTTPS is not used then is value is to be set to __false__ which is the default setting. If HTTPS is to be used the standard HTTPS port is __443__.
* __ssl.key__ - The path to public key.
* __ssl.cert__ - The path to certificate.

There are three environments provided by default: __development__, __test__, and __production__.
Each of these environments has the following configuration options:

* __db__ - This is where you specify the MongoDB / Mongoose settings
* __url__ - This is the url/name of the MongoDB database to use, and is set by default to __mean-dev__ for the development environment.
* __debug__ - Setting this option to __true__ will log the output all Mongoose executed collection methods to your console.  The default is set to __true__ for the development environment.
* __options__ - These are the database options that will be passed directly to mongoose.connect in the __production__ environment: [server, replset, user, pass, auth, mongos] (http://mongoosejs.com/docs/connections.html#options) or read [this] (http://mongodb.github.io/node-mongodb-native/driver-articles/mongoclient.html#mongoclient-connect-options) for more information.
* __app.name__ - This is the name of your app or website, and can be different for each environment. You can tell which environment you are running by looking at the TITLE attribute that your app generates.
* __Social OAuth Keys__ - Facebook, GitHub, Google, Twitter. You can specify your own social application keys here for each platform:
  * __clientID__
  * __clientSecret__
  * __callbackURL__
* __emailFrom__ - This is the from email address displayed when sending an email.
* __mailer__ - This is where you enter your email service provider, username and password.

To run with a different environment, just specify NODE_ENV as you call gulp:
```bash
$ NODE_ENV=test gulp
```
If you are using node instead of gulp, it is very similar:
```bash
$ NODE_ENV=test node server
```
To simply run tests
```bash
$ npm test
```
> NOTE: Running Node.js applications in the __production__ environment enables caching, which is disabled by default in all other environments.

### Logging

As from mean-0.4.4 control over the logging format has been delegated to the env configuration files.
The formats and implementation are done using the morgan node module and it's [predefined format](https://github.com/expressjs/morgan#predefined-formats)
Within each configuration file (config/env/development.js) for instance you state the format in the 'logging' object.
```
'use strict';

module.exports = {
  db: 'mongodb://' + (process.env.DB_PORT_27017_TCP_ADDR || 'localhost') + '/mean-dev',
  debug: true,
  logging: {
    format: 'tiny'
  },
```

The default for the development environment uses [tiny format](https://github.com/expressjs/morgan#tiny)
```
GET /system/views/index.html 304 2.379 ms - -
GET /admin/menu/main 304 8.687 ms - -
GET /system/assets/img/logos/meanlogo.png 304 2.803 ms - -
GET /system/assets/img/backgrounds/footer-bg.png 304 4.481 ms - -
GET /system/assets/img/ninja/footer-ninja.png 304 3.309 ms - -
GET /system/assets/img/logos/linnovate.png 304 3.001 ms - -
```

The production uses the widely used [combined format](https://github.com/expressjs/morgan#combined).
```
:1 - - [22/Mar/2015:13:13:42 +0000] "GET /modules/aggregated.js HTTP/1.1" 200 - "http://localhost:3000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"
::1 - - [22/Mar/2015:13:13:42 +0000] "GET /modules/aggregated.js?group=header HTTP/1.1" 200 0 "http://localhost:3000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"
::1 - - [22/Mar/2015:13:13:42 +0000] "GET / HTTP/1.1" 200 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"
::1 - - [22/Mar/2015:13:13:42 +0000] "GET /modules/aggregated.css HTTP/1.1" 200 - "http://localhost:3000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"
```

## Hosting the project
Since version 0.4.2 MEAN provides a command to easily upload your app to the *mean cloud*.
To do so all you need to do is the following steps.

1. make sure you have a unique name for your app (not the default mean) and that the name is in the package.json
1. Run `mean deploy`
1. It will create the meanio remote which can be used to update your remote app by `git push meanio master`
1. You can add remote command using the --remote flag for instance to add a role to a user on the remote cloud instance run `mean user -a RoleName emailAddress --remote`
1. To get an idea of whats happening on the mean log (node.js based logging) run `mean logs -n 100` to get the last 100 lines...

## Reference Information
  * [Linnovate.net](http://www.linnovate.net/).
  * [Ninja's Zone](http://meanleanstartupmachine.com/)

