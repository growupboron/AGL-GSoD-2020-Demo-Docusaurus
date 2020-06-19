---
edit_link: ''
title: Autobuild
origin_url: >-
  https://git.automotivelinux.org/apps/app-templates/plain/docs/dev_guide/5_autobuild.md?h=flounder
---

<!-- WARNING: This file is generated by fetch_docs.js using /home/boron/Documents/AGL/docs-webtemplate/site/_data/tocs/devguides/flounder/app-templates-guides-flounder-devguides-book.yml -->

# Autobuild script usage

## Generation

To be integrated in the Yocto build workflow you have to generate `autobuild`
scripts using _autobuild_ target.

To generate those scripts proceeds:

```bash
mkdir -p build
cd build
cmake .. && make autobuild
```

You should see _conf.d/autobuild/agl/autobuild_ file now.

## Available targets

Here are the available targets available from _autobuild_ scripts:

- **clean** : clean build directory from object file and targets results.
- **distclean** : delete build directory
- **configure** : generate project Makefile from CMakeLists.txt files.
- **build** : compile all project targets.
- **package** : build and output a wgt package.

You can specify variables that modify the behavior of compilation using
the following variables:

- **CONFIGURE_ARGS** : Variable used at **configure** time.
- **BUILD_ARGS** : Variable used at **build** time.
- **DEST** : Directory where to output ***wgt*** file.

Variable as to be in CMake format. (ie: BUILD_ARGS="-DC_FLAGS='-g -O2'")

Usage example:

```bash
./conf.d/autobuild/wgt/autobuild package DEST=/tmp
```