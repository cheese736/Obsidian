
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

>If it doesn’t make sense, think of it this way, our only goal is to have the subtype class returned in the Parent class(**PersonBuilder**) so that whenver we use the latest subclass we want all its inherited methods **&** to also return the same type as the subcl ass.

---

##  2.  Stepwsie builder
One might encounter situation that the builder should perform a set of steps, one after another in a specific order.


## 3. Functional Builder
- Unlike traditional class builders, we are not required to create a new instance or reset the state every time we want to use the builder. I’ve seen test code become extremely hard to read because the _forEach_ is riddled with building and resetting the state. Even worse, I’ve seen tests covered with reset logic that must run after each test. These are implementation details that we shouldn’t have to manage. The functional builder eliminates these problems.
- 




