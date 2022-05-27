# Unicode Titlecase
Unicode titlecasing operations for chars. The crate supports has additional functionality to
support the TR/AZ locale. 


## Installation
Add this to your `Cargo.toml`:

```toml
[dependencies]
unicode_titlecase = "1.0.0"
```

## Features/Dependencies

There are no dependencies for this crate. The only feature is "std" which is used to add 
```std::Display``` on the iterators. This enables code like 
```'ﬄ'.to_title_case().to_string()```. 

## Usage

To turn a ```char``` into a its titlecase equivalent ```[char; 3]```array:
```rust
use unicode_title_case::to_title_case;

assert_eq!(to_title_case('A'), ['A', '\0', '\0']);
assert_eq!(to_title_case('Ǆ'), ['ǅ', '\0', '\0']);
assert_eq!(to_title_case('ﬄ'), ['F', 'f', 'l']);
```

Or use the iterator version that follows the same format as the std library. The crate defines
a ```Trait``` that is implemented on ```char```:

```rust
use unicode_title_case::TitleCase;
assert_eq!('i'.to_title_case().to_string(), "I");
assert_eq!('A'.to_title_case().to_string(), "A");
assert_eq!('Ǆ'.to_title_case().to_string(), "ǅ");
assert_eq!('ﬄ'.to_title_case().to_string(), "Ffl");
```

### Locale
The TR and AZ locales have different rules for how to titlecase certain characters. 
The ```to_title_case``` functions assume the locale is neither of these locations. For conversions
using TR or AZ locales the following functions are also provided:

```rust
use unicode_title_case::to_title_case_tr_or_az;
assert_eq!(to_title_case_tr_or_az('i'), ['İ', '\0', '\0']);
```
And as an iterator:
```rust
use unicode_title_case::TitleCase;
assert_eq!('i'.to_title_case_tr_or_az().to_string(), "İ");
```

## License

`unicode_title_case` is licensed under the [MIT License](LICENSE)