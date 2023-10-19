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

<BarBottom  title="rust introduction">
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

<BarBottom  title="rust introduction">
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
- Language whirlwind tour
- Ecosystem

</v-clicks>

---
layout: center
class: 'text-center pb-5'
---

# Why?

---
layout: center
class: 'text-center pb-5'
---

## Most loved language on the annual 
## **StackOverflow** survey for _7 years_

---

# Why?

<v-clicks>

- Performance
- Cross platform
- Community and documentation
- No garbage collector
- Growing popularity
- Memory safety
- DX/Tooling

</v-clicks>

---

# Applications of Rust

<v-clicks>

- Systems programming
- Web API's
- Command Line Interface apps (CLI)
- Embedded systems
- WASM
- Linux Kernel

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


- Use `let` to introduce an immutable variable
- Prefix with `mut` to make it mutable
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


Functions which 
- return something, can _optionally_ use `return`
- don't return anything, don't have a return type

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

```rust
let a = [10, 20, 30, 40, 50];

for i in a {
  println!("the value is: {}", i);
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

### Nameless structs

```rust
struct Point(i32, i32);

let origin = Point(0,0);
```

---
layout: center
class: 'text-center pb-5'
---

# Memory (safety) and garbage collection

---

# Memory: Stack v.s. heap

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

# Memory: Stack values

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

# Memory: Heap values

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

# Memory: Ownership of data

- Every _value_ has _one owner_
- There can only be one owner at a time.
- When the owner goes out of scope, value is cleaned/dropped/deallocated

---

# Memory: Ownership of data

```rust
let s1 = String::from("hello");
// owner is moved, s1 no longer valid
let s2 = s1;
```

![picture](/mem1.svg)

---

# Memory: Ownership of data

```rust
let s1 = String::from("hello");
// owner is moved, s1 no longer valid
let s2 = s1;

println!("{}, world!", s1);
```

```
error[E0382]: borrow of moved value: `s1`
 --> src/main.rs:5:28
  |
2 |     let s1 = String::from("hello");
  |         -- move occurs because `s1` has type `String`, which does not implement the `Copy` trait
3 |     let s2 = s1;
  |              -- value moved here
4 |
5 |     println!("{}, world!", s1);
  |                            ^^ value borrowed here after move
```

---

# Memory: Ownership of data

### Fixing it

```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```

---

# Enums

### Simple enumeration

```rust
enum IpAddrKind {
    V4,
    V6,
}

let four = IpAddrKind::V4;

```

### Algebraic data types

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

### Generic algebraic data types

```rust
enum Option<T> {
    None,
    Some(T),
}
```

---

# Pattern matching

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

---

# Result

### Definition

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

### Example usage

```rust
use std::fs::File;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => panic!("Problem opening the file: {:?}", error),
    };
}
```

---

# Unwrap results

```rust
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let mut username_file = File::open("hello.txt")?;
    let mut username = String::new();
    username_file.read_to_string(&mut username)?;
    Ok(username)
}
```

The `?` operator is syntax sugar for `match` on `Ok` and `Err`

---

# Traits: basics

<v-clicks>

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}

```

```rust
pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

```
</v-clicks>

---

# Traits: standard library

<v-clicks>

- Clone
- Debug
- Default
- Eq
- Hash
- Ord

</v-clicks>

---

# Traits: applications

### Derivation of traits

```rust
#[derive(Copy, Clone)]
struct SomeType;
```

### Generic parameter constraining

```rust
fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32
```

### Conversions

```rust
struct Point {
    x: i32,
    y: i32,
}

impl From<(i32, i32)> for Point {
    fn from((x, y): (i32, i32)) -> Self {
        Point { x, y }
    }
}
```

---

# Asynchronous programming

```rust
pub async fn schema_find_by_schema(&self, subject: &String, schema: &String) {
    let avro_schema = AvroSchema::parse_str(schema.as_str())?;
    let fingerprint = avro_schema.fingerprint::<Sha256>().to_string();
    let res = self.repository.schema_find_by_schema(&subject, &fingerprint).await?;

    Ok(res)
}
```

Use `async` + `await` to have asynchronous code. 

- Async code needs an executor
- Implemented by a FSM + polling


---
layout: center
class: 'text-center pb-5'
---

# DX/Tooling

---

# Cargo: summary

<v-clicks>

- Dependency management
- Project configuration
- Building
- Testing
- Documentation

</v-clicks>


---

# Cargo: example

```toml
[package]
name = "rs-schema-registry"
version = "0.1.0"
edition = "2021"

[dependencies]
axum = "0.6.18"
hyper = { version = "0.14.26", features = ["full"] }
tokio = { version = "1.28.1", features = ["full"] }
tower = "0.4.13"
sqlx = { version = "0.7.0-alpha.3", features = [ "runtime-tokio", "tls-rustls", "postgres" ] }
async-trait = "0.1.68"
serde = "1.0.163"
apache-avro = "0.14.0"
sha2 = "0.10.6"
async-recursion = "1.0.4"
```

---

# Libraries

![crates](/crates.png)

---

# Popular libraries

<v-clicks>

- **tokio**: An event-driven, non-blocking I/O platform for writing asynchronous I/O backed applications.
- **sqlx**: An async, pure Rust SQL crate featuring compile-time checked queries without a DSL
- **axum**: Web framework that focuses on ergonomics and modularity
- **serde**: A generic serialization/deserialization framework
- **embassy**: The next-generation framework for embedded applications

</v-clicks>

---
layout: image-x
image: 'https://raw.githubusercontent.com/Fristi/rs-esp32-weatherstation/main/result.jpeg'
imageOrder: 2
---

# rs-esp32-weatherstation

Bare-metal Rust

- ASAIR DHT20 Temperature and Humidity Sensor
- ASAIR AGS02MA TVOC Gas Sensor
- 0.91-inch OLED Display 128*32 pixels white

Reads sensors over i2c and outputs readings on display which is SSD1306 compatabile.

[Github](https://github.com/Fristi/rs-esp32-weatherstation)

---
layout: image-x
image: 'https://miro.medium.com/v2/resize:fit:1400/0*RNcZmLPN5jljq46M.png'
imageOrder: 2
---

# rs-schema-registry

Schema Registry is to enforce data compatibility and enable schema evolution in a decoupled manner.

- SQLX
- Axum
- Serde

Uses idle **15 mb** and **41 mb** under load. *100.000* requests completed with 100 concurrent users with **~9300 request/second** with no tuning.

[Github](https://github.com/vectos/rs-schema-registry)

---
layout: image-x
image: 'https://cdn.shopify.com/s/files/1/0150/6262/products/the_sill-variant-white_gloss-money_tree.jpg?v=1680542101'
imageOrder: 2
---

# mycelium

Automatically watering house plants

Mycelium is a project which consists of a firmware, backend and frontend

- firmware is Rust/ESP32 (I2C, WiFi, BLE)
- frontend is TypeSccript/React/Capacitor (Auth0, BLE)
- backend in Scala (Auth0, Http4s, Doobie)

[Github](https://github.com/Frist/project-mycelium)

---
layout: center
class: 'text-center pb-5'
---

# Thank You!

[https://github.com/Fristi/rust-introduction](https://github.com/Fristi/rust-introduction)