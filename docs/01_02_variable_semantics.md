# Variable Semantics

Grace is a dynamically typed language, in the sense that variables can be reassigned to new values of different types during runtime, but does not introduce unexpected implicit conversions.

Variables in Grace can be declared in two ways - using `var` or using `final`. A `var` can be reassigned, but a `final` cannot.

## `var`

The grammar for a `var` declaration is `"var" IDENTIFIER [ "=" expression ] ";"`.

```
var x = 5;  // x holds an integer
println(x); // prints "5"

x = x * 2;
println(x); // prints "10";

x = "Hello World";  // x has been reassigned to a string, and the integer value has been lost
```

## `final`

The grammar for a `final` declaration is `"final" IDENTIFIER "=" expression ";"`.

```
final x;    // this will produce a compiler error, since a final must be assigned to upon declaration

final name = "Adam";
name = "Sandler";   // this will produce a compiler error, since a final cannot be reassigned to
```

While a `final` cannot be reassigned, you may still assign an object instance to a `final` and call methods on that object that alter the state of the object (objects are covered in more detail in chapter 1.13).

```
class Person:
  var name;

  constructor(n):
    name = n;
  end
end

func set_name(this Person person, new_name):
  person.name = new_name;
end

func main():
  final person = Person("Adam");
  person.set_name("Sandler"); // this method mutates the object and that's still ok even tough person is final
end
```

## Notes

Once a variable is made, the name of that variable cannot be used again in the same scope, and trying so will produce a compiler error.

```
var x = 10;
var x = 20; // compiler error - x already exists

...

func f(x):
  var x;    // compiler error - x already exists as a function parameter
end
```

Trying to use a variable name that does not exist will produce a compiler error.

```
func main():
  println(name);    // compiler error - variable "name" not found
  x = 10;           // compiler error - variable "x" not found
end
```