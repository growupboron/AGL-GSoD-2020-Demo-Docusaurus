---
edit_link: ''
title: Test
origin_url: >-
  https://git.automotivelinux.org/src/xds/xds-docs/plain/docs/part-2/1_xds-server/5_test.md?h=guppy
---

<!-- WARNING: This file is generated by fetch_docs.js using /home/boron/Documents/AGL/docs-webtemplate/site/_data/tocs/devguides/guppy/xds-docs-guides-devguides-book.yml -->

# XDS Server Test

## XDS Server test architecture

The test part is written in go and source code is available in test directory.

```bash
|
+-- test/                # where xds-server test source files
|
+-- test/main_test.go    # main entry point of xds-server test
|
+-- test/fixtures        # fixtures for running test
```

The test execution will locally launch xds-server and access the api through REST and test results, events, ...

## Dependencies

* sshd

Make sure sshd is in your user PATH.

## Launch test

Use the following command to launch test in xds-server root directory:

```bash
make test
```

Launch only one test, for example launch TestSdks:

```bash
make test name=TestSdks
```

Increase test verbosity:

```bash
make test VERBOSE=1
```