# Design Patterns for Node

My ongoing list

- class/instance methods
- chained constructors
- dependency injection using `Object.create`
- method overloading

## Class/Instance Methods

- place the constructors on *Class* function

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

## Chained Constructors

```javascript
Message.NewEmpty = function () {
  return new Message();
}

Message.New = function (from, to, subj, body) {
  var msg = this.NewEmpty();
  msg.from    = from;
  msg.to      = to;
  msg.subject = subj;
  msg.body    = body;
  return msg;  
};

Message.NewFromObject = function (obj) {
  return this.New( obj.from, obj.to, obj.subj, obj.body );
};
```

## Dependency Injection

```javascript
function Server(Connection) {
  //...
}

// server must create new connections
// the constructor will be injected
Server.Connection = null;

Server.New = function () {
  return new Server(this.Connection);
};

function inject(deps) {
  return Object.create(Server, deps);
}

var MyServer = inject({
  Connection: { value: require('./connection') }
});

var server = MyServer.New();
```

## Method Overloading

```javascript
function inject(deps) {
  return Object.create(Server, deps);
}

function defaults() {
  return inject({
    Connection: {
      value: require('./connection')
    }
  });
}

module.exports = function INIT(deps) {
  if (typeof deps === 'object') return inject(deps);
  else if (deps === null)       return defaults();
  else                          throw new Error('injection error');
};
```

