# Value type
A variable of a value type contains an instance of the type. This differs from a variable of a reference type, which contains a reference to an instance of the type. 
By default, on [assignment](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/assignment-operator), passing an argument to a method, and returning a method result, variable values are copied. In the case of value-type variables, the corresponding type instances are copied. The following example demonstrates that behavior:

```C#
using System;

public struct MutablePoint
{
    public int X;
    public int Y;

    public MutablePoint(int x, int y) => (X, Y) = (x, y);

    public override string ToString() => $"({X}, {Y})";
}

public class Program
{
    public static void Main()
    {
        var p1 = new MutablePoint(1, 2);
        var p2 = p1;
        p2.Y = 200;
        Console.WriteLine($"{nameof(p1)} after {nameof(p2)} is modified: {p1}");
        Console.WriteLine($"{nameof(p2)}: {p2}");

        MutateAndDisplay(p2);
        Console.WriteLine($"{nameof(p2)} after passing to a method: {p2}");
    }

    private static void MutateAndDisplay(MutablePoint p)
    {
        p.X = 100;
        Console.WriteLine($"Point mutated in a method: {p}");
    }
}

// Expected output:
// p1 after p2 is modified: (1, 2)
// p2: (1, 200)
// Point mutated in a method: (100, 200)
// p2 after passing to a method: (1, 200)
```

As the preceding example shows, operations on a value-type variable affect only that instance of the value type, stored in the variable.

---
# Reference type
There are two kinds of types in C#: reference types and value types. Variables of reference types store references to their data (objects), while variables of value types directly contain their data. With reference types, two variables can reference the same object; therefore, ==**operations on one variable can affect the object referenced by the other variable**.== With value types, each variable has its own copy of the data, and it's not possible for operations on one variable to affect the other (except in the case of `in`, `ref`, and `out` parameter variables; see [in](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/in-parameter-modifier), [ref](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ref), and [out](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/out-parameter-modifier) parameter modifier).

The following keywords are used to declare reference types:

- [class](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/class)
- [interface](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)
- [delegate](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-delegate-type)
- [record](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record)

C# also provides the following built-in reference types:

- [dynamic](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types)
- [object](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types)
- [string](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types)