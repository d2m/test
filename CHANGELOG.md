## 0.12.5

* Allow `setUp()` and `tearDown()` to be called multiple times within the same
  group.

## 0.12.4+9

* If a `tearDown()` callback throws an error, outer `tearDown()` callbacks are
  still executed.

## 0.12.4+8

* Don't compile tests to JavaScript when running via `pub serve` on Dartium or
  content shell.

## 0.12.4+7

* Support `http_parser` 1.0.0.

## 0.12.4+6

* Fix a broken link in the README.

## 0.12.4+5

* Internal changes only.

## 0.12.4+4

* Widen the Dart SDK constraint to include `1.13.0`.

## 0.12.4+3

* Make source maps work properly in the browser when not using `--pub-serve`.

## 0.12.4+2

* Fix a memory leak when running many browser tests where old test suites failed
  to be unloaded when they were supposed to.

## 0.12.4+1

* Require Dart SDK >= `1.11.0` and `shelf` >= `0.6.0`, allowing `test` to remove
  various hacks and workarounds.

## 0.12.4

* Add a `--pause-after-load` flag that pauses the test runner after each suite
  is loaded so that breakpoints and other debugging annotations can be added.
  Currently this is only supported on browsers.

* Add a `Timeout.none` value indicating that a test should never time out.

* The `dart-vm` platform selector variable is now `true` for Dartium and content
  shell.

* The compact reporter no longer prints status lines that only update the clock
  if they would get in the way of messages or errors from a test.

* The expanded reporter no longer double-prints the descriptions of skipped
  tests.

## 0.12.3+9

* Widen the constraint on `analyzer` to include `0.26.0`.

## 0.12.3+8

* Fix an uncaught error that could crop up when killing the test runner process
  at the wrong time.

## 0.12.3+7

* Add a missing dependency on the `collection` package.

## 0.12.3+6

**This version was unpublished due to [issue 287][].**

* Properly report load errors caused by failing to start browsers.

* Substantially increase browser timeouts. These timeouts are the cause of a lot
  of flakiness, and now that they don't block test running there's less harm in
  making them longer.

## 0.12.3+5

**This version was unpublished due to [issue 287][].**

* Fix a crash when skipping tests because their platforms don't match.

## 0.12.3+4

**This version was unpublished due to [issue 287][].**

* The compact reporter will update the timer every second, rather than only
  updating it occasionally.

* The compact reporter will now print the full, untruncated test name before any
  errors or prints emitted by a test.

* The expanded reporter will now *always* print the full, untruncated test name.

## 0.12.3+3

**This version was unpublished due to [issue 287][].**

* Limit the number of test suites loaded at once. This helps ensure that the
  test runner won't run out of memory when running many test suites that each
  load a large amount of code.

## 0.12.3+2

**This version was unpublished due to [issue 287][].**

[issue 287]: https://github.com/dart-lang/test/issues/287

* Improve the display of syntax errors in VM tests.

* Work around a [Firefox bug][]. Computed styles now work in tests on Firefox.

[Firefox bug]: https://bugzilla.mozilla.org/show_bug.cgi?id=548397

* Fix a bug where VM tests would be loaded from the wrong URLs on Windows (or in
  special circumstances on other operating systems).

## 0.12.3+1

* Fix a bug that caused the test runner to crash on Windows because symlink
  resolution failed.

## 0.12.3

* If a future matched against the `completes` or `completion()` matcher throws
  an error, that error is printed directly rather than being wrapped in a
  string. This allows such errors to be captured using the Zone API and improves
  formatting.

* Improve support for Polymer tests. This fixes a flaky time-out error and adds
  support for Dartifying JavaScript stack traces when running Polymer tests via
  `pub serve`.

* In order to be more extensible, all exception handling within tests now uses
  the Zone API.

* Add a heartbeat to reset a test's timeout whenever the test interacts with the
  test infrastructure.

* `expect()`, `expectAsync()`, and `expectAsyncUntil()` throw more useful errors
  if called outside a test body.

## 0.12.2

* Convert JavaScript stack traces into Dart stack traces using source maps. This
  can be disabled with the new `--js-trace` flag.

* Improve the browser test suite timeout logic to avoid timeouts when running
  many browser suites at once.

## 0.12.1

* Add a `--verbose-trace` flag to include core library frames in stack traces.

## 0.12.0

### Test Runner

`0.12.0` adds support for a test runner, which can be run via `pub run
test:test` (or `pub run test` in Dart 1.10). By default it runs all files
recursively in the `test/` directory that end in `_test.dart` and aren't in a
`packages/` directory.

The test runner supports running tests on the Dart VM and many different
browsers. Test files can use the `@TestOn` annotation to declare which platforms
they support. For more information on this and many more new features, see [the
README](README).

[README]: https://github.com/dart-lang/test/blob/master/README.md

### Removed and Changed APIs

As part of moving to a runner-based model, most test configuration is moving out
of the test file and into the runner. As such, many ancillary APIs have been
removed. These APIs include `skip_` and `solo_` functions, `Configuration` and
all its subclasses, `TestCase`, `TestFunction`, `testConfiguration`,
`formatStacks`, `filterStacks`, `groupSep`, `logMessage`, `testCases`,
`BREATH_INTERVAL`, `currentTestCase`, `PASS`, `FAIL`, `ERROR`, `filterTests`,
`runTests`, `ensureInitialized`, `setSoloTest`, `enableTest`, `disableTest`, and
`withTestEnvironment`.

`FailureHandler`, `DefaultFailureHandler`, `configureExpectFailureHandler`, and
`getOrCreateExpectFailureHandler` which used to be exported from the `matcher`
package have also been removed. They existed to enable integration between
`test` and `matcher` that has been streamlined.

A number of APIs from `matcher` have been into `test`, including: `completes`,
`completion`, `ErrorFormatter`, `expect`,`fail`, `prints`, `TestFailure`,
`Throws`, and all of the `throws` methods. Some of these have changed slightly:

* `expect` no longer has a named `failureHandler` argument.

* `expect` added an optional `formatter` argument.

* `completion` argument `id` renamed to `description`.

##0.11.5+1

* Internal code cleanups and documentation improvements.

##0.11.5

* Bumped the version constraint for `matcher`.

##0.11.4

* Bump the version constraint for `matcher`.

##0.11.3

* Narrow the constraint on matcher to ensure that new features are reflected in
  unittest's version.

##0.11.2

* Prints a warning instead of throwing an error when setting the test
  configuration after it has already been set. The first configuration is always
  used.

##0.11.1+1

* Fix bug in withTestEnvironment where test cases were not reinitialized if
  called multiple times.

##0.11.1

* Add `reason` named argument to `expectAsync` and `expectAsyncUntil`, which has
  the same definition as `expect`'s `reason` argument.
* Added support for private test environments.

##0.11.0+6

* Refactored package tests.

##0.11.0+5

* Release test functions after each test is run.

##0.11.0+4

* Fix for [20153](https://code.google.com/p/dart/issues/detail?id=20153)

##0.11.0+3

* Updated maximum `matcher` version.

##0.11.0+2

*  Removed unused files from tests and standardized remaining test file names.

##0.11.0+1

* Widen the version constraint for `stack_trace`.

##0.11.0

* Deprecated methods have been removed:
    * `expectAsync0`, `expectAsync1`, and `expectAsync2` - use `expectAsync`
      instead
    * `expectAsyncUntil0`, `expectAsyncUntil1`, and `expectAsyncUntil2` - use
      `expectAsyncUntil` instead
    * `guardAsync` - no longer needed
    * `protectAsync0`, `protectAsync1`, and `protectAsync2` - no longer needed
* `matcher.dart` and `mirror_matchers.dart` have been removed. They are now in
  the `matcher` package.
* `mock.dart` has been removed. It is now in the `mock` package.

##0.10.1+2

* Fixed deprecation message for `mock`.

##0.10.1+1

* Fixed CHANGELOG
* Moved to triple-slash for all doc comments.

##0.10.1

* **DEPRECATED**
    * `matcher.dart` and `mirror_matchers.dart` are now in the `matcher`
      package.
    * `mock.dart` is now in the `mock` package.
* `equals` now allows a nested matcher as an expected list element or map value
  when doing deep matching.
* `expectAsync` and `expectAsyncUntil` now support up to 6 positional arguments
  and correctly handle functions with optional positional arguments with default
  values.

##0.10.0

* Each test is run in a separate `Zone`. This ensures that any exceptions that
occur is async operations are reported back to the source test case.
* **DEPRECATED** `guardAsync`, `protectAsync0`, `protectAsync1`,
and `protectAsync2`
    * Running each test in a `Zone` addresses the need for these methods.
* **NEW!** `expectAsync` replaces the now deprecated `expectAsync0`,
    `expectAsync1` and `expectAsync2`
* **NEW!** `expectAsyncUntil` replaces the now deprecated `expectAsyncUntil0`,
    `expectAsyncUntil1` and `expectAsyncUntil2`
* `TestCase`:
    * Removed properties: `setUp`, `tearDown`, `testFunction`
    * `enabled` is now get-only
    * Removed methods: `pass`, `fail`, `error`
* `interactive_html_config.dart` has been removed.
* `runTests`, `tearDown`, `setUp`, `test`, `group`, `solo_test`, and
  `solo_group` now throw a `StateError` if called while tests are running.
* `rerunTests` has been removed.
