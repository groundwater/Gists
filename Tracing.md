# early *early* draft

```javascript
var tracing = require('tracing');
var pro_net = tracing.getProvider('net');
var timers  = tracing.getProvider('timers');

// network tracers //
pro_net.on('connection', 'create', function (srv_handle, con_handle) {
  // srv_handle is the server listening
  // con_handle is the new incoming connection handle
});

pro_net.on('handle', 'read', function (con_handle, buffer, callback) {
  // this connection handle is about to pass buffer to callback
});

pro_net.on('connection', 'destroy', function (handle) {
  // this handle is about to go away
});

// timing tracers //
timers.on('nextTick', 'create', function (callback) {
  // fired after
  // process.nextTick(callback);
  //
  // is there also a timer object for nextTick?
});

timers.on('setImmediate', 'create', function (callback, timer) {
  // i *think* a timer object is created for setImmediate
});

timers.on('setImmediate', 'before', function (callback, timer) {
  // fired *immediately* before the callback
});

timers.on('setImmediate', 'after', function (callback, timer) {
  // fired *immediately* after the callback
});

```
