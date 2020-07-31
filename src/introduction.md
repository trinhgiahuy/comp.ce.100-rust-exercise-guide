# Introduction

## Motivation and structure

Since you're already here, I won't spend too much time discussing ["Why Rust?"](https://doc.rust-lang.org/book/foreword.html)

For the purposes of this course it might be useful to make a really high-level comparison between C and Rust. C is a standard tool in embedded and low-level programming. More than 50 years of history have seen it become abundant, omni-present, in the (more or less) thin layer of software between metal and other software. Rust, on the other hand, was created in the last 10 years. Rust aims to keep what's good with C, and add that which helps make more complex systems more programmable. Much like C and assembly, Rust and C are designed to interoperate, and we are going to take a deep dive into that matter in this course work.

This guide will help you get set up with everything required to run the exercise template on a Windows computer prepared by the course staff, or a personal Linux computer. At the end of the guide there will be some helpful hints on how to do things on embedded Rust.

## This guide will not discuss...
... the following topics, for which you should refer to the main exercise guide:
* exercise specs, exercise requirements,
* board configuration (Development environment tutorial / Board),
* interrupt configurations,
* important memory addresses and bit order,
* led matrix driver explanation,
* reference on course provided function templates (also provided in Rust).
