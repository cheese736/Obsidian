**XPath uses path expressions to select nodes or node-sets in an XML document.**
**These path expressions look very much like the path expressions you use with traditional computer file system.

## XPath Standard Functions

XPath includes over 200 built-in functions.

There are functions for string values, numeric values, booleans, date and time comparison, node manipulation, sequence manipulation, and much more.

Today XPath expressions can also be used in JavaScript, Java, XML Schema, PHP, Python, C and C++, and lots of other languages.

---
Reference: [[https://devhints.io/xpath#selectors]]
# Prefixes

Begin your expression with any of these.

|Prefix|Example|What|
|---|---|---|
|`//`|`//hr[@class='edge']`|Anywhere|
|`./`|`./a`|Relative|
|`/`|`/html/body/div`|Root|

# Decendant selectors

|  |  |   |
|---|---|---|
|`h1`|`//h1`|[?](https://devhints.io/xpath#prefixes)|
|`div p`|`//div//p`|[?](https://devhints.io/xpath#axes)|
|`ul > li`|`//ul/li`|[?](https://devhints.io/xpath#axes)|
|`ul > li > a`|`//ul/li/a`||
|`div > *`|`//div/*`||
|`:root`|`/`|[?](https://devhints.io/xpath#prefixes)|
|`:root > body`|`/body`|


# Using Axes

Steps of an expression are separated by `/`, usually used to pick child nodes. That’s not always true: you can specify a different “axis” with `::`.

```css
//ul/li                       # ul > li
//ul/child::li                # ul > li (same)
//ul/following-sibling::li    # ul ~ li
//ul/descendant-or-self::li   # ul li
//ul/ancestor-or-self::li     # $('ul').closest('li')
```

|   |   |   |   |
|---|---|---|---|
|`//`|`ul`|`/child::`|`li`|
|Axis|Step|Axis|Step|


