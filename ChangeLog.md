Change Log
==========

All notable changes to the project are documented in this file.

[v1.6.0][] - 2016-05-13
-----------------------

### Changes

- Add support for NetBSD `fparaseln()` for the benefit of [Mg][]
- Add support for OpenBSD `reallocarray()` for the benefit of [Mg][]
- Constify `fisdir()` argument


[v1.5.1][] - 2016-04-17
-----------------------

Minor fix release.

### Changes
- Update README.md, add help when libite is used in autotools projects.
  Spell checking and minor cleanup.

### Fixes
- Activate use of `utimensat()` when `pidfile()` is called multiple
  times.  This reduces the overhead of calling open+write+close to
  simply updating the mtime of the PID file.
- Westermo fixes for `fcopyfile()`: nothing copied on embedded PPC
  system when using `tmpfile()` as source.


[v1.5.0][] - 2016-03-20
-----------------------

This release changes the header file namespace.  Apologies for any
problems this may cause!

### Changes
- Change namespace for header files: `libite/` to `lite/`, e.g. using
  `pkg-config` your C program must now `#include <lite/lite.h>`
- Update `pidfile()` to use `utimensat()` to update atime+mtime instead
  of opening and writing PID again.  Less overhead and nanonsecond res.


[v1.4.4][] - 2016-02-23
-----------------------

### Changes
- Add `ibite.pc.in` for `pkg-config` support.

### Fixes
- Fix issue #3: `tempfile()` fails with bad `O_TMPFILE` on some embedded
  targets, in particular PowerPC.  On systems with older GLIBC but with
  a sufficiently new kernel `O_TMPFILE` is missing and the local libite
  definition was wrong, hard coded for x86.  Fixed by Johan Askerin.


[v1.4.3][] - 2016-02-02
-----------------------

### Fixes
- Remove symlinks to Markdown files from GIT
- Distribute and install Markdown files: README.md, etc.


[v1.4.2][] - 2016-01-23
-----------------------

### Fixes
- Fix issue #2: GCC6 `-Wmisleading-indentation` causing FTBFS in pimd,
  which enables `-Werror`


[v1.4.1][] - 2016-01-22
-----------------------

### Fixes
- Fix install path for include files, regression in v1.4.0 With the
  introduction of GNU autotools include file namespace was unfortunately
  lost.  All include files were therefore installed in $(prefix)/include
  instead of $(prefix)/include/libite.


[v1.4.0][] - 2016-01-22
-----------------------

### Changes
- Change to GNU configure and build system
- Add Niels Provos' splay and red-black tree implementation from OpenBSD
  `sys/tree.h`, r1.14
- Make `pidfile()` file name accessible as `__pidfile_name`
- Step ABI revision to 2.1, with help from http://250bpm.com/blog:41


[v1.3.0][] - 2016-01-07
-----------------------

### Changes
- Add highly useful typeless `min()`/`max()` macros to `lite.h`,
  courtesy of Tobias Waldekranz
- Add BSD `queue.h` and Borland inspired `conio.h` to `install-dev`
  target.  Needed by [Finit][].
- Note, this release update `queue.h` to OpenBSD v1.43, which removes
  support for circular queues (CIRCLEQ).
- Update `strlcpy.c` to OpenBSD v1.12, readability fixes.
- Update `strlcat.c` to OpenBSD v1.14, readability fixes.
- Update `strtonum.c` to OpenBSD v1.7, tiniest of style tweaks.

### Fixes
- Only update mtime if `pidfile()` is called more than once, do not
  install multiple `atexit()` handlers.
- Add `#ifndef pidfile`, as for other BSD functions, in case the user
  already have a local copy, or a C library with one.


[v1.2.0][] - 2015-11-23
-----------------------

### Changes
-  Add simple parser for UNIX configuration files, e.g. `/etc/group`,
   `/etc/passwd`, and `/etc/protocols`:
  - `lfopen()`
  - `lfclose()`
  - `lftok()`
  - `lfgetkey()`
  - `lfgetint()`
  - `fgetint()`

### Fixes
- Do not allow `VERSION` to be overloaded by build system.
- Make sure we don't inherit `LDFLAGS` from environment.


[v1.1.1][] - 2015-09-27
-----------------------

### Fixes
* Silence annoying warnings from GNU ar
* Fix macro definitions for compat APIs


[v1.1.0][] - 2015-09-16
-----------------------

### Changes
- Support for `make distdir` used by automake based projects
- `lite.h` move from `error.h` to more BSD friendly `err.h`
- Add highly useful `NELEMS()` and bitmanip macros
- Lots of autotests added
- Add support for running autotests from Travis
- Add `progress()` simple progress bar
- Add `tree()` simple command line tree replacement
- Bump `SONAME` to `libite.so.2` on behalf of [Finit][]

### Fixes
- `pidfile()` upgrade to OpenBSD r1.11
- Lots of README updates, fixes and additions


[v1.0.0][] - 2015-07-12
-----------------------

Initial extraction of frog DNA from [Finit][].  See [README][] for API details.


[UNRELEASED]: https://github.com/troglobit/libite/compare/v1.6.0...HEAD
[v1.6.0]: https://github.com/troglobit/libite/compare/v1.5.1...v1.6.0
[v1.5.1]: https://github.com/troglobit/libite/compare/v1.5.0...v1.5.1
[v1.5.0]: https://github.com/troglobit/libite/compare/v1.4.4...v1.5.0
[v1.4.4]: https://github.com/troglobit/libite/compare/v1.4.3...v1.4.4
[v1.4.3]: https://github.com/troglobit/libite/compare/v1.4.2...v1.4.3
[v1.4.2]: https://github.com/troglobit/libite/compare/v1.4.1...v1.4.2
[v1.4.1]: https://github.com/troglobit/libite/compare/v1.4.0...v1.4.1
[v1.4.0]: https://github.com/troglobit/libite/compare/v1.3.0...v1.4.0
[v1.3.0]: https://github.com/troglobit/libite/compare/v1.2.0...v1.3.0
[v1.2.0]: https://github.com/troglobit/libite/compare/v1.1.1...v1.2.0
[v1.1.1]: https://github.com/troglobit/libite/compare/v1.1.0...v1.1.1
[v1.1.0]: https://github.com/troglobit/libite/compare/v1.0.0...v1.1.0
[v1.0.0]: https://github.com/troglobit/libite/compare/TAIL...v1.0.0
[Finit]:  https://github.com/troglobit/finit/
[Mg]:     https://github.com/troglobit/mg
[README]: https://github.com/troglobit/libite/blob/v1.0.0/README.md

<!--
  -- Local Variables:
  -- mode: markdown
  -- End:
  -->
