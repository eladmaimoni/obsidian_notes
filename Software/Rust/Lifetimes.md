# What Does It Mean?
- On a type - the lifetime of the instance of that type
- On a reference - the reference must be valid for at least as long as the specifier

# Field inside a type:
```
pub struct StrSplit<'a> {
    remainder: &'a str,
    delimiter: &'a str,
}
```
- The `remainder` and `delimiter` must live at least as long as the `StrSplit` instance
- The fields may even live for a longer time, but they should be valid as long as the instance is there
- When the instance is created, the generic lifetime specifier becomes concrete - `'a` becomes the lifetime of the `StrSplit` instance. The compiler enforces that the references inside are valid for the lifetime of the instance.
- This also means that you cannot assign the fields with references that has a shorter lifetime than the instance

