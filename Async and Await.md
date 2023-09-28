[Source](https://blog.stephencleary.com/2012/02/async-and-await.html)

# Introducing the keywords
The "async" keywrod enables the "await" keyword in that method and changes how method results are handled.

**That's all the async keyword does!

It does not run this method on a thread pool thread, or do any other kind of magic. The async keword _only_ enables the await keyword(and manages the method results).

The beginning of an async method is executed just like any other method. That is, it runs synchornously until it hits an "await" (or throws an exception).

The "await" keyword is where thing can get asynchronous. Await is like a ==unary== operator: it takes a single argument, an __awaitable__(an "awaitable" is an asynchronous operation). Await examines that awaitable to see if it has already completed; if the awaitable has already completed, then the method just continues running(synchronously, just like a regular method.)

If "await" sees that the awaitable has not completed, than it acts asynchronously d
