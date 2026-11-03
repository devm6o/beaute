+++
title = 'Rust Ownership in Five Minutes'
date = 2025-11-20T09:00:00Z
description = 'Moves, borrows, and mutable borrows explained with small examples.'
tags = ['rust', 'basics']
+++

Ownership is the idea that makes Rust memory-safe without a garbage collector.
There are three rules:

1. Each value has one owner.
2. When the owner goes out of scope, the value is dropped.
3. You can have many shared borrows **or** one mutable borrow, not both.

## Moves

```rust
fn main() {
    let a = String::from("hello");
    let b = a;            // ownership moves from `a` to `b`
    // println!("{a}");   // error[E0382]: borrow of moved value: `a`
    println!("{b}");
}
```

## Borrowing

Pass a reference when a function only needs to read:

```rust
fn length(s: &str) -> usize {
    s.len()
}

fn main() {
    let name = String::from("ferris");
    println!("{} has {} letters", name, length(&name));
}
```

## Mutable borrowing

```rust
fn shout(s: &mut String) {
    s.push('!');
}

fn main() {
    let mut msg = String::from("hi");
    shout(&mut msg);
    println!("{msg}"); // hi!
}
```

> HINT: When the compiler complains, read the whole error. Rust's messages
> usually point at both the borrow and the place it conflicts.
