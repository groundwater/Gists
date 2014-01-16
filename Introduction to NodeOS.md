# outline

## npm modules

### benefits of npm 

- open/free contribution
- >50k modules
- localized dependencies
- open problems are being actively solved
  1. pre-compilation of module
  2. module signing
  3. private registries

### types of modules

npm accomodates multiple types of packages

#### source modules

- contain `binding.gyp`
- for c++ bindings

#### javascript libraries

- `main` key in `package.json`

#### executables

- `bin` key in `package.json`

#### services

- `scripts:start` key in `package.json`

## npkg - the nodeos package manager

- install a package with `npkg install $pkg`
  - installed to `$home/lib/node_modules`
  - bins are linked to `$home/bin`
- start a service `npkg start $pkg`
- npkg can be used by every user (no root required)
