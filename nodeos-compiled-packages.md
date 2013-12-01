# Packages for NodeOS

NodeOS is a linux distribution that leverages npm as its primary package manager.

Currently there are no compilation tools that work on NodeOS because there are none available on npm.
This means modules with `binding.gyp` files cannot be installed.

There are several approaches to solving this problem:

1. distribute compilation tools on npm
2. extend or replace npm to download pre-compiled modules
3. write an npm proxy that builds or caches compilable modules

The problem with (1) is that unless you compilation tools are entirely javascript you've got a bootstrapping problem. 
You cannot build the build tools without a compiled build tool.

I would rather not do (2) because I want to leverage the npm source as much as possible.
When weighed against (3) it seems like a lot more work.

## The npm proxy

Ues an nginx server that first sees if a local copy of the package exists,
if there is no local cache the request is forwarded to the actual npm server.
Certain packages could be pre-compiled, and their tarballs placed on the proxy server.
This is a relatively transaprent hack that is simple to get running.

### Problems

The problem with the above method is that npm downloads tarballs in two steps.
A package manifest is fetched, which includes a list of versions and the location of their tarballs.
The desired versions is selected from the manifest, and its tarball is fetched.
Even if we point the npm client to our proxy server with `registry = http://my-proxy/` 
the tarball url will point to the original registry.

It seems the only way to overcome this would be by changing the manifest sent to the client.

