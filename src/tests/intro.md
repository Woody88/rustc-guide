# Using the compiler testing framework

The compiler has an extensive testing framework, masterminded by the
compiletest tool (sources in the [`src/tools/compiletest`]). This
section gives a brief overview of how the testing framework is setup,
and then gets into some of the details on
[how to run tests](./tests/running.html#ui) as well as
[how to add new tests](./tests/adding.html).

[`src/tools/compiletest`]: https://github.com/rust-lang/rust/tree/master/src/tools/compiletest

## Test suites

The tests are located in the tree in the [`src/test`]
directory. Immediately within you will see a series of subdirectories
(e.g. `ui`, `run-make`, and so forth). Each of those directories is
called a **test suite** -- they house a group of tests that are run in
a distinct mode.

[`src/test`]: https://github.com/rust-lang/rust/tree/master/src/test

Here is a brief summary of the test suites as of this writing and what
they mean. In some cases, the test suites are linked to parts of the manual
that give more details.

- [`ui`](./tests/adding.html#ui) -- tests that check the exact stdout/stderr from compilation
  and/or running the test
- `run-pass` -- tests that are expected to compile and execute successfully (no panics)
  - `run-pass-valgrind` -- tests that ought to run with valrind
- `run-fail` -- tests that are expected to compile but then panic during execution
- `compile-fail` -- tests that are expected to fail compilation.
- `parse-fail` -- tests that are expected to fail to parse
- `pretty` -- tests targeting the Rust "pretty printer", which
  generates valid Rust code from the AST
- `debuginfo` -- tests that run in gdb or lldb and query the debug info
- `codegen` -- tests that compile and then test the generated LLVM
  code to make sure that the optimizations we want are taking effect.
- `mir-opt` -- tests that check parts of the generated MIR to make
  sure we are building things correctly or doing the optimizations we
  expect.
- `incremental` -- tests for incremental compilation, checking that
  when certain modifications are performed, we are able to reuse the
  results from previous compilations.
- `run-make` -- tests that basically just execute a `Makefile`; the
  ultimate in flexibility but quite annoying to write.
- `rustdoc` -- tests for rustdoc, making sure that the generated files contain
  the expected documentation.
- `*-fulldeps` -- same as above, but indicates that the test depends on things other
  than `libstd` (and hence those things must be built)

## Further reading

The following blog posts may also be of interest:

- brson's classic ["How Rust is tested"][howtest]

[howtest]: https://brson.github.io/2017/07/10/how-rust-is-tested
