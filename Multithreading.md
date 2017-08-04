# Concurrency in C++

`std::async(std::launch, function)` | `std::async(function)`
`std::async` returns a future. Has a launch policy specifying thread creation. `std::launch::async` forces creation of a new thread to be created when called. ``std::launch::deferred` means that code runs only when get or wait is called on the future.
Default policy is the or of the policies which seems odd.

`std::future_status` = `ready` | `deferred` | `timoeout`  
Prioritization is only accessible through `std::thread` API. 


`wait_for` does not force synchronous execution on a deferred aync call. It can be used to check `future_status` and then call `wait` if the status is `deferred`. Honest this seems a bunch a crap.  

`std::thread` = `joinable` | `unjoinable`  
What is this `std::thread` objects corresponding to an underlying thread .. crap
object --> actual thread 

hmm we haven't checked out `std::function`. We should do that  
apostrope as digit separator !

## Thread local storage
