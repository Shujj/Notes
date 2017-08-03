# Exceptions and error handling in C++
[Link to paper](http://stroustrup.com/except.pdf) & [Link to article](https://isocpp.org/wiki/faq/exceptions)
```cpp
try { ... }
catch (ExceptionType1& exception) { ... }
catch (ExceptionType2& exception) { ... }
catch (ExceptionType3& exception) { ... }

```
* make sure you don't forget the & , this will lead to object slicing which will likely not cause an error at compile time but will lead to unitended behaviour. 

* throw accepts a single parameter but is type agnostic (it preserves the type though)
* Constructors typically shouln't pass the buck around for bad intialization.
> Modern C++ implementations reduce the overhead of using exceptions to a few percent (say, 3%) and that’s compared to no error handling. Also all the cost is incurred when you throw an exception: that is, “normal code” is faster than code using error-return codes and tests. You incur cost only when you have an error.
* throw vs assert
> The rule of thumb is that you should use assertions when you are trying to catch your own errors, and exceptions when trying to catch other people's errors. In other words, you should use exceptions to check the preconditions for the public API functions, and whenever you get any data that are external to your system. You should use asserts for the functions or data that are internal to your system.

> Use throw only to signal an error (which means specifically that the function couldn’t do what it advertised, and establish its postconditions).

> Do not use throw if you discover unexpected violation of an invariant of your component, use assert or other mechanism to terminate the program. Throwing an exception will not cure memory corruption and may lead to further corruption of important user data.

> Exceptions, when done right, separate the happy path from the error path.

> In Java, non-memory resources are reclaimed via explicit try/finally blocks. When this mindset is used in C++, it results in a large number of unnecessary try blocks, which, compared with RAII, clutters the code and makes the logic harder to follow. Essentially the code swaps back and forth between the “good path” and the “bad path” (the latter meaning the path taken during an exception). With RAII, the code is mostly optimistic — it’s all the “good path,” and the cleanup code is buried in destructors of the resource-owning objects. This also helps reduce the cost of code reviews and unit-testing, since these “resource-owning objects” can be validated in isolation (with explicit try/catch blocks, each copy must be unit-tested and inspected individually; they cannot be handled as a group).

* Creating custom exceptions
> runtime_error, derived from exception, is the adviced exception class to derive from. This is declared in the stdexcept header. You only have to initialize its constructor with the message you are going to return in the what() method.

what() signature
```cpp
virtual const char* what() const noexcept;
```

* noexcept can have a parameter which compile-time resolves into a boolean. If the boolean is true, then the noexcept sticks. See `is_nothrow_default_constructible<T>::value`. Also it doesn't do any compile time checks for 'throw' statements. The only difference is in runtime behaviour when an exception is raised from a 'noxcept' function.

* don't throw exceptions from constructors
> You can throw an exception in a destructor, but that exception must not leave the destructor; if a destructor exits by emitting an exception, all kinds of bad things are likely to happen because the basic rules of the standard library and the language itself will be violated.

# Linking C++
* Static vs dynamic libraries

# Calling C++ from Java
[Link](https://thebreakfastpost.com/2012/01/21/wrapping-a-c-library-with-jni-introduction/)

Java Native Interface
Proxy class stores the instance of actual class. Store pointer as `long` or `int`.
Load shared lib (.so or .dll)

