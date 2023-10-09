[source](https://www.csharptutorial.net/csharp-tutorial/csharp-events/)

Events are something that occurs in a program. Events allow a class or object to __notify__ other classes or objects when something occurs.
- The class that raises (or sends) the event is called the __publisher__.
- The classes that receive (or handle) the event are called __subscibers__. And the method of the classes that handle the event is often called event handlers.

This pattern is known as __publisher/subscriber__. In this pattern, the publisher determines when to raise the event and the subscribers decide how to handle the event.

Technically, an event has an encapsulated delegate. In fact, an event is like a simpler delegate.

---
## sample code

Suppose we have a class called `Order` with a method `Create()` that creates a new order:

```C#
class Order
{
	public void Create()
	{
		Console.WriteLine("Order Created")
	}
}
```

And two other classes that send an email and SMS:
```C#
class Email
{
	public static void Send()
	{
		Console.WriteLine("Send an email"):
	}
}

class SMS
{
	public static void Send()
	{
		Console.WriteLine("Send an SMS");
	}
}
```

When an order is created, you want to send an email and SMS to the customer. To do it, you may come up with the following code:

```C#
class Order
{
	public void Create()
	{
		Console.WriteLine("Order Created");
		Email.Send();
		SMS.Send();
	}
}
```

Later if you want to do other tasks when an order is created, you have to modify the `Create()` method. Also, the Order class depends on the Email and SMS classes which is not a good design.

To resolve this, you can use the publisher/subcriber pattern:
- The `Order` class is the publisher.
- The `Email` and `SMS` classes are the subscribers.
When an order is created, the `Order` object will notify the `Email` and `SMS` classes to send an email and SMS.

### Declaring an event

The following declares the `Oncreated` event when an order is created:

```C#
delegate void OrderEventHandler();

class Order
{
	public event OrderEventHandler Oncreated;

	public void Create()
	{
		Console.WriteLine("Order created")
	}
}
```
How it works?

1. Define a delegate type for the event.
   
```C#
   delegate void OrderEventHandler():
```

2. Declare an event associated with the delegate type.
   
```C#
public event OrderEventHandler Oncreated;   
```

==Since an event is a member of a class, you need to declare it inside the class.== In this example, the event is public so that other classes can register event handlers with it. Also, the event handlers must match the delegate type associated with the event.


## Raising an event
Raising an event is the same as invoking a method. An event that doesn't have any event handler is null. Therefore, before raising an event, you need to compare it to `null`.

The following raises the `OnCreated` event inside the `Create()` method:

```C#
class Order
{
	public event OderEventHandler OnCreated;

	public void Create()
	{
		Console.WriteLine("Order Created");

		if (OnCreated != null)
		{
			OnCreated();
		}
	}
}
```
