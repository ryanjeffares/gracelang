# Structure of a Grace Program

Unlike some other interpreted languages, Grace does not support a REPL or top level statements. The Grace interpreter must be given a file to run, and that file must contain a `main` function.

```bash
$ grace [options] <file>
```

There are 2 steps in running a Grace program. First, the compiler will read the Grace code and compiler it into bytecode that is held in memory. Secondly, the VM will execute this bytecode. The compiler will report as many errors as possible, mainly syntax errors and calling on local variables that don't exist, but to make the compilation step as fast and seemingly "instant" as possible, there is a lot of error checking that the compiler cannot do, such as type checking, calling non-existent functions, calling functions with the wrong amount of arguments, and calling on class members that do not exist. These errors are reported at runtime.

## Structure of a Grace File

```
// imports must appear at the top of the file.
// any import declarations that come after another
// declaration will produce a compiler error

import std::math;

// the `main` function will be the first thing to run
func main():
  // functions don't have to be forward declared to call
  say_hello();

  println(std::math::sqrti(9));
end

func say_hello():
  println("Hello, World!");
end
```