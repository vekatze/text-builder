# text-builder

`text-builder` is a thin layer over [`binary-builder`](https://github.com/vekatze/binary-builder) to construct texts efficiently.

## Installation

```sh
neut get text-builder https://github.com/vekatze/text-builder/raw/main/archive/0-1-3.tar.zst
```

## Types

### Basics

```neut
data builder {..}

// Allocates memory of size `size` and returns it as a builder.
// The builder's size automatically doubles when there is
// insufficient space to append new data.
define create(size: int): builder

// Extracts the accumulated text from the builder.
define get(b: builder): text
```

### Builders

```neut
// Appends the text `x` to the builder `b`.
define append-text(b: &builder, x: &text): unit

// Appends int64 to the given builder as UTF-8 text.
define append-int64-UTF8(b: &builder, x: int64): unit

// An int32 variant of `append-int64-UTF8`.
define append-int32-UTF8(b: &builder, x: int32): unit

// An int16 variant of `append-int64-UTF8`.
define append-int16-UTF8(b: &builder, x: int16): unit

// Appends int8 to the given builder as UTF-8 text.
define append-int8-UTF8(b: &builder, x: int8): unit

// Appends float64 to the given builder as UTF-8 text.
define append-float64-UTF8(b: &builder, x: float64): unit

// An float32 variant of `append-float64-UTF8`.
define append-float32-UTF8(b: &builder, x: float32): unit

// An float16 variant of `append-float64-UTF8`.
define append-float16-UTF8(b: &builder, x: float16): unit
```

## Example

```neut
define zen(): unit {
  let b = create(4) in
  let _ on b =
    append-text(b, "hello");
    append-int64-UTF8(b, 123);
    append-text(b, "world")
  in
  let result = get(b) in
  printf("{}\n", [result])
}

// => hello123world
```
