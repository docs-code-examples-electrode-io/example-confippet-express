# example-confippet-express
* This repo is an example express.js app with [electrode-confippet] module fully integrated
* The step-by-step instructions on building it from scratch can be found below

## Electrode Confippet
[electrode-confippet] is a versatile utility for managing your NodeJS application configuration. Its goal is customization and extensibility, but offers a preset config out of the box.

## yeoman + express-generator
* This app was scaffolded using [yeoman] and [express-generator]
* First, install `yeoman` and `express-generator`:

```bash
npm install -g yo
npm install -g express-generator
```

* Scaffold a new app using `yeoman`:

```bash
express expressApp
cd expressApp
npm install
```

* At this point, you should be able to run the server locally:

```bash
NODE_ENV=development npm start
```

## Electrode Confippet

```bash
npm install electrode-confippet --save
```

### Config Files
* Create the config folder:

```bash
mkdir config
cd config
```

* Add the following config files:

```
config
|_ default.json
|_ development.json
|_ production.json
```

* Add your configuration settings
* Update the `config/default.json` to have the following settings:

```
{
  "server": {
    "viewCache": false,
    "xPoweredBy": true,
    "port": 3000
  }
}
```

### Development Environment
* Update the `config/development.json` to have the following settings:

```
{
  "server": {
    "viewCache": false,
    "xPoweredBy": true,
    "port": 4000
  }
}
```

* The above settings disable view cache, enable x-powered-by header and run the server in port 4000

### Production Environment
* Update the `config/production.json` to have the following settings:

```
{
  "server": {
    "viewCache": true,
    "xPoweredBy": false,
    "port": 8000
  }
}
```

* The above settings enable view cache, disable x-powered-by header and run the server in port 8000
* Keys that exist in the `config/default.json` that are also in the other environment configs will be replaced by the environment specific versions

### Confippet Require
* Add the following to app.js:

```
const config = require("electrode-confippet").config;

app.set("view cache", config.server.viewCache);
app.set("x-powered-by", config.server.xPoweredBy);
app.listen(config.server.port);
```

### Running the Express app
* Start the express app in `development` environment:

```
NODE_ENV=development npm start
```

* Start the express app in `production` environment:

```
NODE_ENV=production npm start
```

* Running in the selected environment should load the appropriate configuration settings

Built with :heart: by [Team Electrode](https://github.com/orgs/electrode-io/people) @WalmartLabs.

[electrode-confippet]: https://github.com/electrode-io/electrode-confippet
[yeoman]: yeoman.io
[express-generator]: https://github.com/expressjs/generator