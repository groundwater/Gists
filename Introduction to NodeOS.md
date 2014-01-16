# Outline

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

## npkg - the nodeOS package manager

- install a package with `npkg install $PKG`
  - installed to `$HOME/lib/node_modules`
  - bins are linked to `$HOME/bin`
- start a service `npkg start $PKG`
- npkg can be used by every user (no root required)
