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

