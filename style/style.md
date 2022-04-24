# Grace Styling

This file contains guidelines on styling Grace code.

## Naming

* Classes in Grace should be named with `PascalCase`
```
class poorly_named_class: // bad
end

class WellNamedClass:     // good
end
```
* Functions and variables in Grace should be named with `snake_case`
```
func poorlyNamedFunction(PoorlyNamedArg):  // bad 
	var poorlynamedlocal;
end

func well_named_function(well_named_arg):  // good
	var well_named_local;
end
```
* `static` fields should be named with `UPPER_SNAKE_CASE`
```
static PoorlyNamedStatic = 1;  // bad
static WELL_NAMED_STATIC = 1;  // good
```
* No user defined types, functions, or variables should ever start with a double underscore (`__`) as this is reserved for internal use
```
class __PoorlyNamedClass:  // bad
end
```

## Variables
* It is good practice to use `final` over `var` wherever possible (prefer immutability)
```
func factorial(n):  // bad - n should be final
  if n < 2:
	return 1;
  end
  return n + factorial(n - 1);
end

func fib(final n):  // good - n doesn't need to be mutable
  if n < 2:
    return n;
  end
  return fib(n - 2) + fib(n - 1);
end
```

## Spacing and Indentation
* Whitespace and indentation are ignored by the Grace compiler except where it changes the meaning or validity of an expression, for example:
```
final x = 10*2==20;  // valid
final y = x < = 30;  // error at `=` - `<=` operator can't have space 
```
* However, indentation and line breaks should remain consistent within a project and with the guidelines
* All blocks (`func`, `if`, `for`, `while`, `class`) should have a line break after the trailing `:`
* The `end` token for each of these blocks should appear on its own line
```
if x: println("hello"); end  // bad

if x:                        // good
  println("hello");
end
```
* A new level of indentation should appear after each new block opens, and indentation should ideally be 2 spaces
```
func say_hello():
println("hello");        // bad - no indentation  
end

func say_goodbye():
	println("goodbye");  // bad - indentation is 4 spaces
end

func say_hi():
  println("hi");         // good - indentation is 2 spaces
end
```
