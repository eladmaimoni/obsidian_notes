# Callbacks and enable_shared_from_this
Prolog:
- Why callbacks are hard - separation of time and space
Slides:
1. **Be careful when passing `this` to a callback**.
   - example: how 'this' may dangle when you use callbacks
   - lifetime issues - the callback may outlive `this`
2. **Consider `enable_shared_from_this` when using callbacks**
   - explain that in fact we have **shared ownership** of `this`: the callback and the owner of the class
   - how `enable_shared_from_this` helps
   - `shared_ptr` threading guarantee (a single thread will call the destructor)
3. **Use `weak_from_this` instead of `shared_from_this` to pass `this` to callbacks**
   - easy to create cyclic dependency when using `shared_from_this`
4. **Enforce making `shared_from_this` only via `make_shared` (private key / token)**
5. **Be careful of accidental private inheritance when using `enable_shared_from_this`**
# Coroutines
Prolog: 
- short explanation of the most common coroutine structure (like async / await that exist on other languages)
- explain the 3 parts of a "common" coroutine:
  - pre `co_await`
  - 'async gap'
  - continuation
-  explain where the stack sits (stackless coroutine)
  
  Slides
1. **Be aware of the current thread when returning from `co_await`**
   - may start on the current thread, and return on a different one entirely
   - you may access your class members from multiple threads without intending to.
   - misleading because many languages have built-in mechanism to return on the same thread
2. **Never pass by reference to a coroutine**
   - show that the coroutine stack will contain references, but they will dangle once they live the scope of the initial invocation
3. **Never co_await inside a lambda**
   - dummy thread pool example where the lambda dies after the pool invokes it, but the continuation 
4. optional: 'joiner' pattern for waiting for a coroutine to stop.

# Threads
Prolog: 
- Discuss how to write a class containing `std::thread` / `std::jthread`
- What do we usually want from this class?
  - thread safety
  - easy to reason about
  - structured way to pass data to the thread
  - clear separation between memory accessed by the thread and the outside world
  - a clean way to Start / Stop the thread and even: Restart its operation
    
Basically - the simple pattern I use to write classes that uses threads (Session Pattern)

Other ideas:
- be careful of std::shared_ptr::use_count()