- Used as building block for other (safer) interior mutability constructs
- Allows you to get a raw mutable pointer to `T`, that you can unsafely dereference to a mutable reference.
- I think it returns a raw pointer by purpose, so you would have to use unsafe code to dereference it into a reference (mutable / shared). This way, if you violate the borrowing rules than rust can say it emanated from unsafe block.

### `get` vs. `get_mut`
- `get` returns a pointer, we must use unsafe code to get a mutable reference to the inner value.
- `get_mut` returns a mutable reference, and can be used without unsafe code.
- `get` operates on `&self` meaning it is a "const" function that does not require the `UnsafeCell` to be mutable.
- `get_mut` requires the `UnsafeCell` to be mutable. This is not very useful as it implies that we have an exclusive reference to the `UnsafeCell` and therefore it is SAFE to change its internals.

### Example: violating exclusive references:
```
    let i1 = std::cell::UnsafeCell::new(5);

	// obtain 2 mutable references
    let i1_ref1 = unsafe { &mut *i1.get() };
    let i1_ref2 = unsafe { &mut *i1.get() };

    *i1_ref1 = 6;
    *i1_ref2 = 7;

    print!("values: {} {}\n", i1_ref1, i1_ref2); // print 7, 7 
```

### How to use properly:
- you must not create a construct that will violate the borrowing rules (you can!)
- `Cell` implements a "scoped" usage of mutable references. it only borrows `T` inside the `set` method that mutates it.
- `Cell` never returns a reference (shared  / exclusive) to the user. So it always knows there are no references to `T` and hence it can be changed within the `set` function.
- `RefCell` does return a reference to the user. But it tracks the reference usage manually and panics if it is violated.

