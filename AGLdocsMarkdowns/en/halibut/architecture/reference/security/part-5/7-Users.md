---
edit_link: ''
title: Users
origin_url: >-
  https://raw.githubusercontent.com/automotive-grade-linux/docs-sources/halibut/docs/security-blueprint/part-5/7-Users.md
---

<!-- WARNING: This file is generated by fetch_docs.js using /home/boron/Documents/AGL/docs-webtemplate/site/_data/tocs/architecture/halibut/security_blueprint-security-blueprint-book.yml -->

# Users

The user policy can group users by function within the car. For example, we can
consider a driver and his passengers. Each user is assigned to a single group to
simplify the management of space security.

## Root Access

The main applications, those that provide the principal functionality of the
embedded device, should not execute with root identity or any capability.

If the main application is allowed to execute at any capability, then the entire
system is at the mercy of the said application's good behaviour. Problems arise
when an application is compromised and able to execute commands which could
consistently and persistently compromise the system by implanting rogue
applications.

It is suggested that the middleware and the UI should run in a context on a user
with no capability and all persistent resources should be maintained without any
capability.

One way to ensure this is by implementing a server-client paradigm. Services
provided by the system's drivers can be shared this way. The other advantage of
this approach is that multiple applications can share the same resources at the
same time.

<!-- section-config -->

Domain                | Object           | Recommendations
--------------------- | ---------------- | -----------------------------------------------------
Platform-Users-root-1 | Main application | Should not execute as root.
Platform-Users-root-2 | UI               | Should run in a context on a user with no capability.

<!-- end-section-config -->

Root access should not be allowed for the following utilities:

<!-- section-config -->

Domain                | `Utility` name | _State_
--------------------- | -------------- | -------------
Platform-Users-root-3 | `login`        | _Not allowed_
Platform-Users-root-4 | `su`           | _Not allowed_
Platform-Users-root-5 | `ssh`          | _Not allowed_
Platform-Users-root-6 | `scp`          | _Not allowed_
Platform-Users-root-7 | `sftp`         | _Not allowed_

<!-- end-section-config -->

Root access should not be allowed for the console device. The development
environment should allow users to login with pre-created user accounts.

Switching to elevated privileges shall be allowed in the development environment
via `sudo`.

--------------------------------------------------------------------------------

<!-- pagebreak -->

## Capabilities

<!-- section-todo -->

Domain                        | Improvement
----------------------------- | ------------------------
Platform-Users-Capabilities-1 | Kernel or Platform-user?
Platform-Users-Capabilities-2 | Add config note.

<!-- end-section-todo -->

The goal is to restrict functionality that will not be useful in **AGL**. They
are integrated into the **LSM**. Each privileged transaction is associated with
a capability. These capabilities are divided into three groups:

- e: Effective: This means the capability is “activated”.
- p: Permitted: This means the capability can be used/is allowed.
- i: Inherited: The capability is kept by child/subprocesses upon execve() for example.
