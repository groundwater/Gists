> I think config files are an anti-pattern in node

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
