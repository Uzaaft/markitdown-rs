# markitdown-rs

markitdown-rs is a Rust library designed to facilitate the conversion of various document formats into markdown text. It is a Rust implementation of the original [markitdown](https://github.com/microsoft/markitdown) Python library.

## Features

It supports:

- [x] Excel(.xlsx)
- [ ] Word
- [ ] PowerPoint
- [x] PDF
- [ ] Images
- [ ] Audio
- [ ] HTML
- [ ] Text-based formats (plain text, .csv, .xml, .rss, .atom)
- [ ] ZIP

## Installation

Add the following to your `Cargo.toml`:

```toml
[dependencies]
markitdown = "0.1.0"
```

## Usage

### Initialize MarkItDown

```rust
use markitdown::MarkItDown;

let mut md = MarkItDown::new();
```

### Convert a File

```rust
use markitdown::{ConversionOptions, DocumentConverterResult};

let options = ConversionOptions {
    file_extension: Some(".xlsx".to_string()),
    url: None,
};

let result: Option<DocumentConverterResult> = md.convert("path/to/file.xlsx", Some(options));

if let Some(conversion_result) = result {
    println!("Converted Text: {}", conversion_result.text_content);
} else {
    println!("Conversion failed or unsupported file type.");
}
```

### Register a Custom Converter

You can extend MarkItDown by implementing the `DocumentConverter` trait for your custom converters and registering them:

```rust
use markitdown::{DocumentConverter, MarkItDown};

struct MyCustomConverter;

impl DocumentConverter for MyCustomConverter {
    // Implement the required methods here
}

let mut md = MarkItDown::new();
md.register_converter(Box::new(MyCustomConverter));
```

## License

MarkItDown is licensed under the MIT License. See `LICENSE` for more details.
