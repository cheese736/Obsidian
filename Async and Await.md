[Source](https://blog.stephencleary.com/2012/02/async-and-await.html)

# Introducing the keywords

The "async" keyword enables the "await" keyword in that method and changes how method results are handled.

**That's all the async keyword does!

It does not run this method on a thread pool thread, or do any other kind of magic. The async keyword _only_ enables the await keyword(and manages the method results).

The beginning of an async method is executed just like any other method. That is, it runs synchronously until it hits an "await" (or throws an exception).

The "await" keyword is where thing can get asynchronous. Await is like a ==unary== operator: it takes a single argument, an __awaitable__(an "awaitable" is an asynchronous operation). Await examines that awaitable to see if it has already completed; if the awaitable has already completed, then the method just continues running(synchronously, just like a regular method.)

If "await" sees that the awaitable has not completed, then it acts asynchronously. It tells the awaitable to run the remainder of the method when it completes and then _returns_ from the async method.

Later on, when the awaitable completes, it will execute the remainder of the async method. If you're awaiting a built-in awaitable(such as a task), then the remainder of the async method will execute on a "context" that was captured before the "await" returned.

I like to think of "await" as an "asynchronous wait". That is to say, the async method pauses until the awaitable is complete(so it waits), but the actual thread is not blocked(so it's asynchronous).


# Awaitables

As I mentioned, "await" takes a single argument - an "awaitable" - which is an asynchronous operation. There are two awaitable types already common in the .NET framework: Task<T> and Task.

There are also other awaitable types: special methods such as "Task.yield" return awaitables that are not Tasks, and the WinRT runtime(coming in Windows 8) has an unmanaged awaitable type. You can also create your own awaitable(usually for performance reasons), or use extension methods to make a non-awaitable type awaitable
