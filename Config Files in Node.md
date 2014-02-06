> I think config files are an anti-pattern in node

## Introduction

No application ships *exactly* as you want it.

- application, config, environment, user-data
  1. application is source code, often released by developers at fixed points
  2. config generally done by ops, or developer (config is same between dev/staging/production)
  3. environment by ops (differs by host)
  4. user-data by users (often bound to environment)
- configuration is separate from user data
- two predominant styles
  - source config files (e.g. nginx)
  - binary-serialized config files (e.g. iOS)
- source files can be complex, like meta-programming (e.g. nginx)
- binary serialization is difficult to automate (am I forced to use GUI?)

Why not just program the app *exactly* as needed?

- many dynamic platforms
- for compiled apps, most servers don't have compilation tool chains

## Config

> configuration by dependency injection

Use the *root* file as your config file, but configure your app by wiring modules together directly.

```javascript
// server.js
var options = {
  username: process.env.USERNAME || 'default',
  password: process.env.PASSWORD || 'hunter2'
};
require('./app.js').start(options);
```

### A Better Config

Even better, pass in fully-configured objects.

```javascript
// server.js
var options = {
  auth: require('./auth.js').init(process.env.USERNAME, process.env.PASSWORD)
}
require('./app.js').start(options);
```

In the above example, anything that meets the interface provided by `options.auth` can be substituted in.
