https://play.rust-lang.org/evaluate.json

{
  "code" : "// This code is editable and runnable!\nfn main() {\n    println!(\"Hello World\");\n}\n"
}


-----

{
    "result": "Hello World\n"
}



Slide notes:


---

What is Rust
Why it exists

## Hello World
```rust
fn main() {
  println!("Hello World");
}
```

## Variables + mutability

```rust
fn main() {
  let x = 1;
  let y = "ARGS";
  let z = [1, 2, 3, 4, 5];
}
```

Mutability
```rust
fn main() {
  let x = 1;
  x += 1;
  println!("X: {}", x);
}
```

```rust
fn main() {
  let mut x = 1;
  x += 1;
  println!("X: {}", x);
}
```

## Borrowing

```rust
fn main() {
  let mut x = 1;
  let mut x_ref = &mut x;

  *x_ref += 1;

  println!("XREF: {}", x_ref);
}
```
OK


```rust
fn main() {
  let mut x = 1;
  let mut x_ref = &mut x;

  *x_ref += 1;

  println!("XREF: {}", x_ref);
  println!("X: {}", x);
}
```
Errors

Can use scopes...

```rust
fn main() {
  let mut x = 1;

  {
    let mut x_ref = &mut x;
    *x_ref += 1;
    println!("XREF: {}", x_ref);
  }

  println!("X: {}", x);
}
```
RAII

## Functions

## Enums + Values

Data type with several possible variants

```rust
enum Direction {
  North,
  South,
  East,
  West
}

fn main() {
  let direction = Direction::North;
}

```

Can optionally have data associated with it
```rust
enum Message {
    Quit,
    ChangeColour(u8, u8, u8),
    Move { x: i32, y: i32 },
    Write(String),
}

fn main() {
  let change_message = Message::ChangeColour(255, 255, 255);
  let move_message =   Message::Move { x: 10, y: 100 };
  let write_message =  Message::Write("Hello World".to_string());
  let quit_message =   Message::Quit;
}
```

## Tuples

## Pattern Matching

```rust
fn main() {
  let x = 5;

  let result = match x {
      1 => "one",
      2 => "two",
      3 => "three",
      4 => "four",
      5 => "five",
      _ => "something else",
  };

  println!("Mumbo number {}", result);
}
```

Now with enums (non-exhaustive):

```rust
enum Message {
    Quit,
    ChangeColour(u8, u8, u8),
    Move { x: i32, y: i32 },
    Write(String),
}

fn process_message(message: Message) {
    match message {
        Message::ChangeColour(r, g, b) => println!("Changing colour to [{},{},{}]", r, g, b),
        Message::Move { x: x, y: y }   => println!("Move to [{},{}]", x, y),
        Message::Write(s)              => println!("{}", s),
    };
}

fn main() {
  process_message(Message::ChangeColour(255, 255, 255));
  process_message(Message::Move { x: 10, y: 100 });
  process_message(Message::Write("Hello World".to_string()));
}


```

All variants must be implemented.

```rust
enum Message {
    Quit,
    ChangeColour(u8, u8, u8),
    Move { x: i32, y: i32 },
    Write(String),
}

fn process_message(message: Message) {
    match message {
        Message::ChangeColour(r, g, b) => println!("Changing colour to [{},{},{}]", r, g, b),
        Message::Move { x: x, y: y }   => println!("Move to [{},{}]", x, y),
        Message::Write(s)              => println!("{}", s),
        _                              => println!("Unknown Command"),
    };
}

fn main() {
  process_message(Message::ChangeColour(255, 255, 255));
  process_message(Message::Move { x: 10, y: 100 });
  process_message(Message::Write("Hello World".to_string()));
  process_message(Message::Quit);
}

```

Pattern matching with Tuples

## No null/nil

```rust
const TURTLE_POSITION: (f32, f32) = (3.0, 3.0);

#[derive(Debug)]
enum Turtle {
  Happy,
  Sad
}

fn find_nearby_turtle(search_position: (f32, f32), radius: f32) -> Option<Turtle> {
  if distance(TURTLE_POSITION, search_position) < radius {
    return Some(Turtle::Happy)
  }
  None
}

fn distance(pos_a: (f32, f32), pos_b: (f32, f32)) -> f32 {
  let x_diff = pos_b.0 - pos_a.0;
  let y_diff = pos_b.1 - pos_a.1;

  ((x_diff * x_diff) + (y_diff * y_diff))
}

fn main() {
  let search_position = (3.0, 3.0);
  let found_turtle = find_nearby_turtle(search_position, 1.0);
  println!("Found turtle?: {:?}", found_turtle)
}

```

Structs + Traits

```rust
struct Position {
  x: f32,
  y: f32
}

fn main() {
  let position = Position { x: 1.0, y: 1.0 };
}
```

```rust
struct Position {
  x: f32,
  y: f32
}

impl Position {
  pub fn new(x: f32, y: f32) -> Position {
    Position { x: x, y: y }
  }
}

fn main() {
  let position = Position::new(1.0, 1.0);
}
```

Box + Heap allocation
Async Patterns
References and Moved data
Lifetimes
Generics + Trait Objects
