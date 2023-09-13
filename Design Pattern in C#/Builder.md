
# Motivation
- Some objects are simple and can be created in a single constructor call.
- Other objects require a lot ceremony to create
-  Having an object with 10 constructor arguments is not productive.
- Instead, opt for piecewise construction.
- Builder provides an API for constructing an object step-by-step.


> **When piecewise object construction is complicated, provide an API for doing it succinctly. 

A fluent interface: an interface which allow you to chain serveral calls by returning a reference to the object you are working

# Fluent Builder Inheritance with Recursive Generics

## 1. The Problem With the Fluent Builder Inheritance
Image we want to build an `Employee` object:
```c#
public class Employ
{
	public string Name {get; set; }
	public string Position {get; set; }
}
```

To continue on, we are going to create a *builder class* to bulid the `Name` part of our object:

```C#
public class EmployeeInfoBuilder
{
	protected Employee employee = new Employee();
	public EmployeeInfoBuilder SetName(string name)
	{
		employee.Name = name;
		return this;
	}
}
```

Now create another builder class to build the `Position` part

```C#
public class EmployeePositionBuilder : EmployeeInfoBuilder
{
	public EmployeePositionBuilder AtPosition(string position)
	{
		employee.Position = position;
		return this;
	}
}
```

But, as we can see, we are not able to create a required object. This is because the `SetName` method will return an instance of type `EmployeeInfoBuilder` which currently doesn’t implement or inherit the `AtPosition` method. This is quite okay since the `EmployeeInfoBuilder` class is a higher order class and the `EmployeePositionBuilder` class inherits from it, and not another way around.

So, we need to find a solution ==to propagate information from the derived class to the base class==. And the solution is in **recursive generics** approach.





