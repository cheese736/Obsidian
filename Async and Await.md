[Source](https://blog.stephencleary.com/2012/02/async-and-await.html)

# Introducing the keywords

The "async" keyword enables the "await" keyword in that method and changes how method results are handled.

**That's all the async keyword does!

It does not run this method on a thread pool thread, or do any other kind of magic. The async keyword _only_ enables the await keyword(and manages the method results).

The beginning of an async method is executed just like any other method. That is, it runs synchronously until it hits an "await" (or throws an exception).

The "await" keyword is where thing can get asynchronous. Await is like a ==unary== operator: it takes a single argument, an __awaitable__(an "awaitable" is an asynchronous operation). Await examines that awaitable to see if it has already completed; if the awaitable has already completed, then the method just continues running (synchronously, just like a regular method.)

If "await" sees that the awaitable has not completed, then it acts asynchronously. It tells the awaitable to run the remainder of the method when it completes and then _returns_ from the async method.

Later on, when the awaitable completes, it will execute the remainder of the async method. If you're awaiting a built-in awaitable (such as a task), then the remainder of the async method will execute on a "context" that was captured before the "await" returned.

I like to think of "await" as an "asynchronous wait". That is to say, the async method pauses until the awaitable is complete (so it waits), but the actual thread is not blocked (so it's asynchronous).


# Awaitables

As I mentioned, "await" takes a single argument - an "awaitable" - which is an asynchronous operation. There are two awaitable types already common in the .NET framework: `Task<T>` and `Task`.

There are other awaitable types: special methods such as `Task.yield`return awaitables that are not Tasks, and the WinRT runtime (coming in Windows 8) has an unmanaged awaitable type. You can also create your own awaitable (usually for performance reasons), or use extension methods to make a non-awaitable type awaitable.

One Important point about awaitables is this: it is the ==_type_== that is awaitable, not the ==_method_== returning the type. In other words, you can await the result of an async method that returns Task ... because the method returns Task, not because it's async. __So you can await the result of a non-async method that returns Task.__

# Return Types

Async methods can return `Task<T>`, `Task`, or `void`. In almost all cases, you want to return `Task<T>` or Task, and return void only when you have to.
Why return `Task<T>` or `Task`? Because they are awaitable, and void is not. So if you have an async method returning `Task<T>` or `Task`, then you can pass the result to await. With a void method, you don't have anything to pass to wait.
You have to return void when you have async event handlers.

