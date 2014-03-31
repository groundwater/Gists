# Design Patterns for Node

My ongoing list

- class/instance methods
- chained constructors
- dependency injection using `Object.create`
- method overloading

## Class/Instance Methods

- place the constructors on *Class* function
- only initialize data in the constructor

```javascript
function Message () {
  this.from    = null;
  this.to      = null;
  this.subject = null;
  this.body    = null;
}

Message.NewEmpty = function () {
  return new Message();
}
```

Rather than call `new Message()` you call `Message.New()`.
This keeps the `function Message() {...}` body clean,
and lets you create multiple constructors.

```javascript
Message.NewReply = function (message, body) {
  var reply     = new Message();

  reply.from    = message.to;
  reply.to      = message.from;
  reply.subject = "RE: " + message.subject;
  reply.body    = body;

  return reply;
}
```

## Chained Constructors

- only call `new` in one constructor
- for each way to create an object, create a new constructor
- avoid re-using logic, instead delegate to other constructors

```javascript
Message.NewEmpty = function () {
  return new Message();
}

Message.New = function (from, to, subj, body) {
  var msg     = this.NewEmpty();

  msg.from    = from;
  msg.to      = to;
  msg.subject = subj;
  msg.body    = body;

  return msg;  
};

Message.NewReply = function (message, body) {
  var from    = message.to;
  var to      = message.from;
  var subject = "RE: " + message.subject;
  var body    = body;

  return this.New(from, to, subj, body);
};
```

## Dependency Injection

*here is the advanced maneuver*

Inject dependencies that you would normally reference via `require`.

```javascript
function Server() {
  this.name = null;
}

Server.prototype.createConnection = function (host) {
  return this.$.request(host);
};

/* the below is basically boilerplate */

Server.New = function () {
  return Object.defineProperty(new Server(), '$', {value: this});
};

function inject(deps) {
  return Object.create(Server, deps);
}

// default dependencies
function defaults() {
  return {
    request: {
      value: require('some-request-module')
    }
  };
}

module.exports = function INIT(deps) {
  return inject(deps || defaults());
};
```
