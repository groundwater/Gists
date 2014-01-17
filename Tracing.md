# early *early* draft

```javascript
var tracing  = require('tracing');
var pro_net = tracing.getProvider('net');

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
```
