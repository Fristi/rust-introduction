---
layout: cover
theme: purplin
highlighter: shiki
colorSchema: light
---

# Rust

<p text="2xl" class="!leading-8">
An introduction to Rust
</p>

<div class="abs-br mx-14 my-12 flex">
  <!-- <logos:vue text="3xl"/> -->
  <div class="ml-3 flex flex-col text-left gap-1">
    <div class="text-sm opacity-50">October 2023</div>
  </div>
</div>

<BarBottom  title="zio-test">
  <Item text="">
    <img
      src="https://vectos.net/img/logo.png"
      class="w-16"
    />
  </Item>
</BarBottom>

---
layout: 'intro'
---

<h1 text="!5xl">Mark de Jong</h1>

<div class="leading-8 opacity-80">
Functional Programming 🥑<br>
Company site: <a href="https://vectos.net" target="_blank">Vectos</a>.<br>
</div>

<img src="https://vectos.net/img/mark.jpg" class="rounded-full w-40 abs-tr mt-30 mr-20"/>

<BarBottom  title="zio-test">
  <Item text="">
    <img
      src="https://vectos.net/img/logo.png"
      class="w-16"
    />
  </Item>
</BarBottom>


---

# Agenda

<v-clicks>

- Why?
- History
- Language whirlwind tour
- Cargo

</v-clicks>

---

# Why?

<v-clicks>

- Performance
- Cross platform
- Community and documentation
- No garbage collector
- Growing popularity
- Memory safety
- WASM

</v-clicks>

---

# Applications of Rust

<v-clicks>

- Linux Kernel
- Systems programming
- Web API's
- Command Line Interface apps (CLI)
- Embedded systems

</v-clicks>

---
layout: center
class: 'text-center pb-5'
---

# Language whirlwind tour

---

# Data types - numbers

### integers

|Length|Signed|Unsigned|
|---|---|---|
|8-bit|`i8`|`u8`|
|16-bit|`i16`|`u16`|
|32-bit|`i32`|`u32`|
|64-bit|`i64`|`u64`|
|128-bit|`i128`|`u128`|

### float

For floating point numbers there is `f32` and `f64`

---

# Data types - primitives

### bool

No suprises, there's a `bool` type which introduces `true` and `false`

### char

The `char` type representes a single character.

### array

```rust
let a: [i32; 5] =[1, 2, 3, 4, 5]
```

- They have a fixed length, `5` in this case
- Their elements can be accessed by index like: `a[0] == 1`

---


# Variables

```rust
let a = 5;
let mut b = 10;

const HOUR_IN_SECONDS = 3600;
```


- Use `let` to introduce a variable
- Immutable by default
- Use `mut` to make it mutable
- Use `const` to introduce a constant (always immutable)

---


# Functions

```rust
fn add(a: i32, b: i32) -> i32 {
  a + b
}

fn do_something() {
  println!("I don't return anything, but I do print")
}
```


- Functions which return something, can optionally use `return`
- Functions which don't return anything, don't have any return type

---

# Control flow

### `if` expressions

```rust
let number = 3;

if number < 5 {
    println!("number is < 5");
} else {
    println!("number is >= 5");
}
```

### binding `if` to `let`

```rust
// inline
let condition = true;
let b = if condition { 5 } else { 6 };
```

---

# Control flow

### loop

```rust
fn main() {
    loop {
        println!("again!");
    }
}
```

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result} {counter}");
}
```

---

# Control flow

### Conditional loop `while`

```rust
let mut number = 3;

while number != 0 {
    println!("{number}!");
    number -= 1;
}

println!("LIFTOFF!!!");
```

---

# Control flow

### Loop through collection

```rust
let a = [10, 20, 30, 40, 50];
let mut index = 0;

while index < 5 {
    println!("the value is: {}", a[index]);

    index += 1;
}
```

---

# Structs

### Named

```rust
struct User {
  active: bool,
  sign_in_count: u32
}

let fred = User { active: false, sign_in_count: 42 };
```

### Unitless

```rust
struct Point(i32, i32);

let origin = Point(0,0);
```

---

# Stack v.s. heap

### Stack

- Is ordered
- Last In, First out (LIFO)
- Operations are fast
- Values on the stack have a fixed size (known at compile time)

### Heap

- Less organized
- Operations are slower
- Values on the heap are dynamic (size _not_ known at compile time)

---

# Stack values

```rust
let x: i32 = 42;
let name: &str = "Alice";

struct Point {
  x: f64,
  y: f64
}

let origin = Point { x: 0.0, y: 0.0 }

```

---

# Heap values

```rust
let string = String::from("Heap allocated string");
let vector = vec![1, 2, 3];
let boxed = Box::new(42);

struct Person {
  name: String,
  age: u16
}

let person = Person { name: String::from("Mark"), age: 1337 }

```



---

# Ownership of data

- Every _value_ has _one owner_
- There can only be one owner at a time.
- When the owner goes out of scope, value is cleaned/dropped/deallocated

---

# Enums

---

# Pattern matching

---

# Option

---

# Result

---

# Unwrap

---

# Traits

---

# Asynchronous programming




---
layout: center
class: 'text-center pb-5'
---

# Thank You!

[https://github.com/Fristi/rust-introduction](https://github.com/Fristi/rust-introduction)