By default, Rust brings only a few types into the scope of every program in the prelude. 
The `std::prelude::v1` includes the following:

* `std::marker`::{`Copy, Send, Sized, Sync, Unpin`}. The marker traits indicate fundamental properties of types.
* `std::ops`::{`Drop, Fn, FnMut, FnOnce`}. Various operations for both destructors and overloading ().
* `std::mem`::`drop`, a convenience function for explicitly dropping a value.
* `std::boxed`::`Box`, a way to allocate values on the heap.
* `std::borrow`::`ToOwned`, The conversion trait that defines `to_owned`, the generic method for creating an owned type from a borrowed type.
* `std::clone`::`Clone`, the ubiquitous trait that defines clone, the method for producing a copy of a value.
* `std::cmp`::{`PartialEq, PartialOrd, Eq, Ord `}. The comparison traits, which implement the comparison operators and are often seen in trait bounds.
* `std::convert`::{`AsRef, AsMut, Into, From`}. Generic conversions, used by savvy API authors to create overloaded methods.
* `std::default`::`Default`, types that have default values.
* `std::iter`::{`Iterator, Extend, IntoIterator, DoubleEndedIterator, ExactSizeIterator`}. Iterators of various kinds.
* `std::option`::`Option`::{`self, Some, None`}. A type which expresses the presence or absence of a value. This type is so commonly used, its variants are also exported.
* `std::result`::`Result`::{`self, Ok, Err`}. A type for functions that may succeed or fail. Like Option, its variants are exported as well.
* `std::string`::{`String, ToString`}, heap allocated strings.
* `std::vec`::`Vec`, a growable, heap-allocated vector.

Notes:

1. The `::` syntax in `T::f` line indicates that `f` is an associated function of the `T` type
2. `String::new` is a function that returns a new instance of a String. 
3. `String` is a string type provided by the standard library that is a growable, UTF-8 encoded bit of text.
4. The `&` indicates that this argument is a reference, which gives you a way to let multiple parts of your code access one piece of data without needing to copy that data into memory multiple times. 
5. Like variables, references are immutable by default. Hence, you need to write `&mut guess` rather than `&guess` to make it mutable


# Cargo Version Number

## [semantic versioning](https://semver.org)

The version number `0.5.5` in the `[dependencies]` section of `Cargo.toml` is actually a shorthand of `^0.5.5`, which means “any version that has a public API compatible with version 0.5.5.”

## Cargo.lock file

Ensuring Reproducible Builds with the Cargo.lock File. Cargo.lock file was created the first time you ran cargo build and will stay in your project directory. 
When you build a project for the first time, Cargo figures out all the versions of the dependencies that fit the criteria and then writes them to the Cargo.lock file. 
When you build your project in the future, Cargo will see that the Cargo.lock file exists and use the versions specified there rather than doing all the work of figuring out versions again. This lets you have a reproducible build automatically. In other words, your project will remain at 0.5.5 until you explicitly upgrade, thanks to the Cargo.lock file.

# Updating a Crate to Get a New Version

```bash
cargo update
```

This will ignore the Cargo.lock file and figure out all the latest versions that fit your specifications in Cargo.toml. If that works, Cargo will write those versions to the Cargo.lock file.

But by default, Cargo will only look for greater patch versions rather than greater minor versions, e.g. if originally 0.5.5, then `update` will only look for 0.5.x where x>5.

# Reference, Variables

Suppose you want to define an immutable variable `x` and a mutable variable `y`. 
```rust
let x = 0;
let mut y = 0;
```

`&x` indicates a reference to the immutable variable while `&mut y` indicates a reference to the mutable variable `y`. 
All references are immutable by default.
When passing a reference as an argument of a function, this is a way to let multiple parts of your code access one piece of data without needing to copy that data into memory multiple times. 


# Result types

`read_line` puts what the user types into the string we’re passing it, but it also returns a value—in this case, an `io::Result`

Rust has a number of types named `Result` in its standard library: a generic `Result` as well as specific versions for submodules, such as `io::Result`.

The `Result` types are `enumerations`, often referred to as `enums`. An enumeration is a type that can have a fixed set of values, and those values are called the enum’s `variants`.

For `Result`, the variants are `Ok` or `Err`. The `Ok` variant indicates the operation was successful, and inside Ok is the successfully generated value. The `Err` variant means the operation failed, and `Err` contains information about how or why the operation failed.


An instance of `io::Result` has an `expect` method that you can call. If this instance of `io::Result` is an `Err` value, expect will cause the program to crash and display the message that you passed as an argument to `expect`. If the `read_line` method returns an `Err`, it would likely be the result of an error coming from the underlying operating system. If this instance of `io::Result` is an `Ok` value, `expect` will take the return value that `Ok` is holding and return just that value to you so you can use it. In this case, that value is the number of bytes in what the user entered into standard input.


# Placeholder `{}`

```rust
println!("You guessed: {}", guess);
```

The set of curly brackets, {}, is a placeholder: think of {} as little crab pincers that hold a value in place. You can print more than one value using curly brackets: the first set of curly brackets holds the first value listed after the format string, the second set holds the second value, and so on

# Reviewing docs for a method

 You won’t just know which traits to use and which methods and functions to call from a crate. Instructions for using a crate are in each crate’s documentation. Another neat feature of Cargo is that you can run the `cargo doc --open` command, which will build documentation provided by all of your dependencies locally and open it in your browser. If you’re interested in other functionality in the rand crate, for example, run `cargo doc --open` and click rand in the sidebar on the left.

# Infinite loop

```rust
    loop{


    }
```

 # Comparison in std

 `std::cmp::Ordering`, like `Result`, is another enum, but the variants for `Ordering` are `Less`, `Greater`, and `Equal`, which are the three outcomes that are possible when you compare two values.

# match block

 We use a `match` expression to decide what to do next based on which variant of `Ordering` was returned from the call to `cmp` with the values in `guess` and `secret_number`

 ```rust
    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
 ```

Codes after `=>` in a `match` block can be a statement or a block of statements. 

```rust
    loop{
        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
```

# Variable Shadowing

Rust allows us to shadow the previous value of a variable with a new one. This feature is often used in situations in which you want to convert a value from one type to another type

```rust
    let mut guess = String::new();

    io::stdin().read_line(&mut guess)
        .expect("Failed to read line");

    let guess: u32 = guess.trim().parse()
        .expect("Please type a number!");
```

The `parse` method on strings parses a string into some kind of number. Because this method can parse a variety of number types, we need to tell Rust the exact number type we want by using `let guess: u32`. The colon (`:`) after guess tells Rust we’ll annotate the variable’s type. 

Rust has a few built-in number types; the u32 seen here is an unsigned, 32-bit integer. It’s a good default choice for a small positive number. 


# Using match block for error handling:

Remember that `parse` returns a `Result` type and `Result` is an enum that has the variants `Ok` or `Err`. Previously, we use `expect` method to handle both `Ok` and `Err`. But what if we want to handle them on our own?

Here, instead of calling `expect` on the `Result` type, we can use a `match` block:

```rust
        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };
```

This equals to 

```rust
        let guess_rst : Result = guess.trim().parse();
        let guess: u32 = match guess_rst {
            Ok(num) => num,
            Err(_) => continue,
        };
```

Here, `continue` gives us more control on the flow of the program, but a single `expect` method call wouldn't.



