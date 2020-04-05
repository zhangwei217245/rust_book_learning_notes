By default, Rust brings only a few types into the scope of every program in the prelude. 
The `std::prelude::v1` includes the following:

`std::marker`::{`Copy, Send, Sized, Sync, Unpin`}. The marker traits indicate fundamental properties of types.
`std::ops`::{`Drop, Fn, FnMut, FnOnce`}. Various operations for both destructors and overloading ().
`std::mem`::`drop`, a convenience function for explicitly dropping a value.
`std::boxed`::`Box`, a way to allocate values on the heap.
`std::borrow`::`ToOwned`, The conversion trait that defines `to_owned`, the generic method for creating an owned type from a borrowed type.
`std::clone`::`Clone`, the ubiquitous trait that defines clone, the method for producing a copy of a value.
`std::cmp`::{`PartialEq, PartialOrd, Eq, Ord `}. The comparison traits, which implement the comparison operators and are often seen in trait bounds.
`std::convert`::{`AsRef, AsMut, Into, From`}. Generic conversions, used by savvy API authors to create overloaded methods.
`std::default`::`Default`, types that have default values.
`std::iter`::{`Iterator, Extend, IntoIterator, DoubleEndedIterator, ExactSizeIterator`}. Iterators of various kinds.
`std::option`::`Option`::{`self, Some, None`}. A type which expresses the presence or absence of a value. This type is so commonly used, its variants are also exported.
`std::result`::`Result`::{`self, Ok, Err`}. A type for functions that may succeed or fail. Like Option, its variants are exported as well.
`std::string`::{`String, ToString`}, heap allocated strings.
`std::vec`::`Vec`, a growable, heap-allocated vector.

Notes:

3. The `::` syntax in `T::f` line indicates that `f` is an associated function of the `T` type
1. `String::new` is a function that returns a new instance of a String. 
2. `String` is a string type provided by the standard library that is a growable, UTF-8 encoded bit of text.
4. The `&` indicates that this argument is a reference, which gives you a way to let multiple parts of your code access one piece of data without needing to copy that data into memory multiple times. 
5. Like variables, references are immutable by default. Hence, you need to write `&mut guess` rather than `&guess` to make it mutable
