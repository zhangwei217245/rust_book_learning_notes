# Installation on Linux/MacOS

```bash
curl https://sh.rustup.rs -sSf | sh
```

logout and login

## Updating rust

```bash
rustup update
```

## local doc

```bash
rustup doc
```

# HelloWorld

main.rs:

```rust
fn main() {
    println!("Hello, world!");
}
```

## Compile and run:

```bash
rustc main.rs
./main
```

## Notes:

1. Functions start with keyword `fn`, then function name, parameter list wrapped with parentheses `()`, then function body wrapped with curly brackets `{}`
2. all statements end with semicolon `;`
3. all macro calls end with `!`

# Cargo

Cargo is Rust’s build system and package manager.

## Creating a Project with Cargo

```bash
cargo new <project_name>
```

Cargo.toml is just like pom.xml in Maven but written in TOML format. 

## Cargo build and run

```bash
cargo build # build the cargo project, by default its a debug version and the result will be stored in target/debug
cargo run # run the main function in src/main.rs
```

```bash
cargo build --release # build release version
```

