# Debian builds for Travis

The debian builds are stored here so that Travis can grab them.

## To update:

* Fire up Ubuntu 20.  (Whichever method works for you, i.e. direct/VM/docker/...)
   * *NOTE:  If you want to use a different version of Ubuntu, edit [https://github.com/sys-bio/roadrunner/blob/develop/.travis.yml](roadrunner/.travis.yml) so that it has a new 'dist' instead of 'dist:focal', which is Ubuntu 20.  See https://docs.travis-ci.com/user/reference/overview/*
* Clone this repository to that machine.
* Clone and build the https://github.com/sys-bio/libroadrunner-deps repository to that machine.
* When configuring libroadrunner-deps in CMake, set CMAKE_INSTALL_PREFIX to /path/to/deps-for-travis/libroadrunner-deps/usr/  (Alternatively, copy the install to that directory afterwards)
* Build and install libroadrunner-deps
* Edit libroadrunner-deps/DEBIAN/control to use a new version number, if necessary, and push those changes.
* run the following commands:
   * ```dpkg-deb --build libroadrunner-deps```
   * ```mv libroadrunner-deps.deb libroadrunner-deps_2.0.9_amd64.deb```  (or use the new version number)
* If the filename has changed, delete the old one and add the new one, and edit [https://github.com/sys-bio/roadrunner/blob/develop/.travis.yml](roadrunner/.travis.yml) to point wget at the new version.
* Push the changes to git.
* Edit this README file to reflect any changes that might have happened.
