## Constants

*This section is currently inaccurate - expressions are not supported in constant declarations, only single literal values*

Constants serve as a way to alias a constant value that does not change during runtime with a readable name. Constants are "folded" during the compilation step - so using a named constant will compile to the same bytecode as using a literal value.

```
const PI = 3.141592653589793;
const TWO_PI = PI * 2;

func main():
  println(TWO_PI);  // no variable lookup is performed here - the constant 6.28... is inserted into the bytecode
end
```

A constant must be set to a literal value of builtin primitive type (more information in chapter 1.4) or the result of an expression containing only primitive literals or other predefined constants.

```
const NAME = "Adam" + "Sandler";    // valid
const NUMS = [0, 1, 2];             // invalid, lists cannot be constants
```