# Patched dependencies for winapi crates

This directory contains two folders, `x86_64` and `i686`. These two folders are
used to define crates which override the `winapi-{i686,x86_64}-pc-windows-gnu`
crates on crates.io. The intention is that we use these patched crates instead
of the versions on crates.io with a `[patch]` in the `src/Cargo.toml` workspace
definition.

These overrides are currently necessary because otherwise Cargo fails to compile
on the MinGW targets. These crates on crates.io provide a number of import
libraries, such as `libws2_32.a`, which are added to the link path via the build
scripts in the crates. These import libraries, however, override the versions
provided by MinGW (such as `/mingw64/x86_64-w64-mingw32/lib/libws2_32.a`) which
are required to link correctly.

You can find an [example failure][fail] as well as a [brief discussion][comment]
of the issue online as well. Note that this directory is intended to be a
temporary solution to be removed soon.

[fail]: https://ci.appveyor.com/project/rust-lang/rust/build/1.0.6017/job/pgow2cfxp4a7k9l2
[comment]: https://github.com/rust-lang/rust/pull/47280#issuecomment-357476725
