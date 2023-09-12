
## Motivation
- Some objects are simple and can be created in a single constructor call.
- Other objects require a lot ceremony to create
-  Having an object with 10 constructor arguments is not productive.
- Instead, opt for piecewise construction.
- Builder provides an API for constructing an object step-by-step.


> **When piecewise object construction is complicated, provide an API for doing it succinctly. 

A fluent interface: an interface which allow you to chain serveral calls by returning a reference to the object you are working

## Fluent Builder Inheritance with Recursive Generics

sample code:
```c#
public class Person
{
	public string Name { get; set; }
	public string Position { get; set; }
}

public class PersonInfoBuilder
{
	protected Person persion = new Person();
	public PersonInfoBuilder Called(string name)
}



```