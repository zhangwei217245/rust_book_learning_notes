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




