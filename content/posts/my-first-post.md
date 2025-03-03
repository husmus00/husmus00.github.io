---
title: "Getting Started with The Rust FFI"
date: 2024-03-25T14:24:12+03:00
draft: false
favorite: false
slug: "rust-ffi"
description: Communicating with C code through Rust
author: "Hussam"
categories:
tags:
- Rust
- Embedded
---

## Getting Started with The Rust FFI
<br>
After spending some time experimenting with Rust's FFI, I thought I'd write a short article on getting started with it, pointing to some useful resources and tools.

<br>

The Rust FFI (Foreign-Function Interface) provides a way for Rust code to natively "talk" to C code and C APIs / libraries. This makes it possible to use Rust in existing C projects and allows for communicating directly with existing OS APIs (e.g., POSIX, WinAPI). This involves using types provided in the standard library (std::ffi) or core::ffi when using no_std on bare metal.

<br>

To call C code from Rust, a function definition must be provided within an `extern "C"` block, similar to the signature of the actual C function. This function signature will be written in Rust but must use types provided by the FFI instead of Rust's native types (e.g., c_int over i32).

To call Rust code from C, a Rust function must be defined as `pub extern "C"` and must use C types in its signature. The #[no_mangle] annotation must also be used to ensure the Rust compiler doesn't change the function name during compilation. For more details, see [this](https://docs.rust-embedded.org/book/interoperability/index.html) page from The Embedded Rust Book.

<br>

Note that interoperating with external code requires using an `unsafe` block as the compiler cannot provide safety guarantees for non-Rust code.

I believe the FFI should be seen as a tool to help transition to Rust, rather than an excuse not to use it when it eventually makes life difficult :)
Rust does have a steeper learning curve than C, but its benefits are well worth the investment.

<br>

[The Rust Embedded Book]((https://docs.rust-embedded.org/book/index.html)) is a great place to learn more about the FFI and dealing with no_std.

* Some useful resources:
1. [libc](https://github.com/rust-lang/libc):
Provides an interface to the C standard library for the FFI and can work in no_std environments.

2. [nix](https://github.com/nix-rust/nix):
A higher-level wrapper around libc for *nix systems, providing a safer abstraction.

3. [cc-rs](https://github.com/rust-lang/cc-rs):
A build-stage tool that makes it easy to include C files within Rust's build process by communicating with the platform's C compiler.

4. [rust-bindgen](https://github.com/rust-lang/rust-bindgen):
A tool to automatically generate FFI bindings from a C header file.
https://lnkd.in/gP8hX9vF


The next thing I want to do is experiment with the [embedded-hal](https://github.com/rust-embedded/embedded-hal), to learn how to use Rust to communicate directly with embedded hardware.


