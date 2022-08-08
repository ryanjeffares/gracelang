# Builtin Primitive Types

Grace has 5 builtin primitive types: `Int`, `Float`, `Bool`, `Char`, `String`, and `Null`.

## `Int`

An `Int` will be produced from an integer literal or an expression containing other integers or variables/constants holding integers, for example `5`, `23 * 3`, `10 / 3`.

Division with two integers will perform an integer division, no implicit conversion to `Float` will happen if both operands are integers.

`Int`s in Grace are 64 bit signed integers, with a minimum value of -9,223,372,036,854,775,808 and a maximum value of 9,223,372,036,854,775,807 (inclusive). An integer literal outside of this range will produce a compiler error since it cannot be parsed. **NB: The behaviour of creating an integer outside of this range during runtime is defined by the C++ compiler used to compile the interpreter. Integer overflow is possible.**

## `Float`

A `Float` will be produced from a float literal (number containing a decimal point) or an expression containing numbers where at least 1 is a float, for example `1.23`, `10 / 3.0`, `23 * 6.0 / 2`.

`Float`s in Grace are 64 bit floats (`double`s in the C++ implementation) with a range of 1.7E-308 to 1.7E+308. A literal outside of this range cannot be parsed.

## `Bool`

A `Bool` is produced from a `true` or `false` literal or the result of a logical expression, for example `5 == 5`, `(10 / 3) <= 3.5`.

`Bool`s cannot be implicitly converted to numbers like in C/C++, but casts are available.

```
var f = false;
var t = true;

var x = Int(f);     // returns 0
var y = Float(t);   // returns 1.0
var z = Bool(10);   // returns true for any non zero values
```