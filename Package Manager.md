npm is pretty great, but here are my ideas for improving it

- namespace accounts a la github `jacob/ssh`
- store tarballs at eternally unique urls using sha-1 hashes
- the package website is really just a social network for packages and users
  1. star/favorite packages
  2. comment/discuss packages
  3. integrate with github issues
  4. link forked packages across accounts e.g. `jacob/ssh -> sofia/ssh`
- create curl'able indexes for looking up build artifcats

The `pkg` executable does *not* use the website, only the index it has been linked to.
Indexes are there to serve different platforms, e.g. `linux-x64` or `smartos-x86`.

## package resolution

- loosely couple package resolution

*Why?* because modules should be treated as modules.
Modules should not *go get* other modules via require.
They should *accept* dependencies via injection.

**Note** that the require syntax *does not* need to change.
We definitely do *not* want RequireJS.

Abstractly, think of each module as having a mapping from names to other modules.
Those other modules are dependencies passed in by the `require` statement.
As long as that mapping can be remapped on-demand, you can treat require as a dependency injector.

**inject a module object**

```javascript
var stubs = {
  'net': netStub
};
var mysql = require.withModules(stubs)('mysql');
// mysql has a stubbed out 'net' module
```

**remap a module**

```javascript
var map = {
  'db': 'node_modules/mysql'
};
var db = require.withMap(map)('db');
```

## package resolution

Right now packages are downloaded to `node_modules`.
Requiring the package `bubbles` will automatically search `node_modules`, 
regardless of where you are in the tree.

- treat all top-level directories like `node_modules`

Requiring a module like `require('xy')` will find the `xy` module in any top-level directory

```
package.json
index.js
node_modules/
my_modules/
  xy/
    package.json
    index.js
```

Modules can be required in a uniform way, but assembled according to their relationship to the project.
Modules in `package.json` will still go to `node_modules`,
but you can divide your project into small modules and place them into another directory.
Relative require still works.

You can logically separate:

- modules installed by `npm install`
- 3rd party modules checked into git
- custom modules for the project

