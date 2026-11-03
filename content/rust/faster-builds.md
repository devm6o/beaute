+++
title = 'Speeding Up Rust Builds'
date = 2026-04-03T09:00:00Z
description = 'Practical settings to cut Rust compile times during development.'
tags = ['rust', 'performance', 'tooling']
+++

Rust compile times add up. These changes make the edit, build, and test loop
noticeably faster.

## Use `cargo check` while editing

`cargo check` type-checks without generating code. It is much faster than
`cargo build` when you only want to know whether the code compiles.

## Find out where the time goes

```bash
cargo build --timings
```

This writes an HTML report showing how long each crate took and which ones
blocked the others.

## Optimize dependencies, not your code

Dependencies rarely change, so compiling them with optimizations once is
cheap, and it makes debug builds run faster:

```toml
# Cargo.toml
[profile.dev.package."*"]
opt-level = 2
```

## Use a faster linker

Linking is often the slowest step of an incremental build. On Linux,
[mold](https://github.com/rui314/mold) is a drop-in replacement:

```toml
# .cargo/config.toml
[target.x86_64-unknown-linux-gnu]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=mold"]
```

## Remove duplicate dependencies

```bash
cargo tree --duplicates
```

Two versions of the same crate are compiled twice. Aligning versions in
`Cargo.toml` is an easy win.
