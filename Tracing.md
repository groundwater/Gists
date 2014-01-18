# early *early* draft

```javascript
var tracing = require('tracing');

// network tracers //
tracing.on('net', 'connection:create', function (srv_handle, con_handle) {
  // srv_handle is the server listening
  // con_handle is the new incoming connection handle
});

tracing.on('net', 'handle:read', function (con_handle, buffer, callback) {
  // this connection handle is about to pass buffer to callback
});

tracing.on('net', 'handle:destroy', function (handle) {
  // this handle is about to go away
});

// timing tracers //
tracing.on('timers', 'nextTick:create', function (callback) {
  // fired after
  // process.nextTick(callback);
  //
  // is there also a timer object for nextTick?
});

tracing.on('timers', 'setImmediate:create', function (callback, timer) {
  // i *think* a timer object is created for setImmediate
});

tracing.on('timers', 'setImmediate:before', function (callback, timer) {
  // fired *immediately* before the callback
});

tracing.on('timers', 'setImmediate:after', function (callback, timer) {
  // fired *immediately* after the callback
});

```

**implementing a trace**

```javascript
// this is a wondeful module global that represents the
// current context/continuation in play
var current = {};

tracing.on('net', 'connection:create', function (srv_handle, con_handle) {
  // associate this handle with a new continuation
  // we associate its continuation with the same continuation that
  // the server had when it started listening
  con_handle._continuation = { parent: srv_handle._continuation };
});

tracing.on('net', 'handle:onread', function (con_handle, buffer, callback) {
  // we're about to enter `callback`
  // switch the current continuation with the connection handle's
  current = con_handle._continuation;
});

tracing.on('timers', 'setImmediate:create', function (callback, timer) {
  // this timer inherits the current continuation
  timer._continuation = { parent: current };
});

tracing.on('timers', 'setImmediate:before', function (callback, timer) {
  current = timer._continuation;
});
```
