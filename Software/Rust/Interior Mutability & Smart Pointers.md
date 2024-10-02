- in rust, you can only change a value if you have a `&mut T` type of reference to it
- the compiler enforce that only a single mutable reference exists at any moment
- there are wrappers that allow multiple owners to mutate a value. they typically allow for a some sort of scoped access to mutate the value - such as `Mutex` and its single threaded variant `Cell`
- The ability to have a 'shareable reference' (`&T`) that allows multiple owners while allowing the type to be mutated is called interior mutability

### Cell
- used for single threaded access - does not implement Sync
- allows to multiple entities to own the cell, like a shared_ptr in single threaded environment
- each entity can mutate the value within the cell - in a synchronous manner so there is no ability to change it multiple types
Can you give someone a mutable reference to a cell?
- Yes, this means he can change the cell itself (by assigning a new Cell to it for example)
- Yet, it can't obtain a mutable reference to the value