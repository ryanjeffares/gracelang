# Builtin Primitive Types

Grace has 5 builtin primitive types: `Int`, `Float`, `Bool`, `Char`, `String`, and `null`.

## `Int`

An `Int` will be produced from an integer literal or an expression containing other integers or variables/constants holding integers, for example `5`, `23 * 3`, `10 / 3`.

Division with two integers will perform an integer division, no implicit conversion to `Float` will happen if both operands are integers.

`Int`s in Grace are 64 bit signed integers, with a minimum value of -9,223,372,036,854,775,808 and a maximum value of 9,223,372,036,854,775,807 (inclusive). An integer literal outside of this range will produce a compiler error since it cannot be parsed. **NB: The behaviour of creating an integer outside of this range during runtime is defined by the C++ compiler used to compile the interpreter. Integer overflow is possible.**

Grace has support for binary and hexadecimal literals that can be parsed as integers.

```
println(0xFFFF);        // prints 65535
println(0b11001110);    // prints 206
```

Bitwise operations - shift left/shift right `<<`/`>>`, bitwise or `|`, bitwise and `&`, bitwise xor `^`, complement `~` - can be performed on `Int`s and *only* `Int`s.

```
println(1 << 32);           // prints 4294967296
println(0b0101 | 0b1010);   // prints 15
println(~2);                // prints -3
```

## `Float`

A `Float` will be produced from a float literal (number containing a decimal point) or an expression containing numbers where at least 1 is a float, for example `1.23`, `10 / 3.0`, `23 * 6.0 / 2`.

`Float`s in Grace are 64 bit floats (`double`s in the C++ implementation) with a range of 1.7E-308 to 1.7E+308. A literal outside of this range cannot be parsed.

## `Bool`

A `Bool` is produced from a `true` or `false` literal or the result of a logical expression, for example `5 == 5`, `(10 / 3) <= 3.5`.

`Bool`s cannot be implicitly converted to numbers like in C/C++, but explicit casts are available.

```
var f = false;
var t = true;

println(t * 10);    // will not result in 10 like in C, instead is a runtime error

var x = Int(f);     // returns 0
var y = Float(t);   // returns 1.0
var z = Bool(10);   // returns true for any non zero values
```

## `Char`

A `Char` will be produced from a single character literal (a single character or (valid) escaped character between single quotes `'*'`), or an expression that returns a character. `Char`s in Grace are stored as `char`s in C++, so the values that can be parsed and stored depend on the C++ implementation.

`Char`s cannot be used as integers in most expressions. Further information is given on the behaviour of operators in Grace in chapter 1.05, but for example, multiplying a `Char` by an `Int` will produce a `String`.

```
println('a' * 5);       // prints aaaa
println('a' + 'b');     // prints ab
println('a' + 10);      // runtime error
```

## `String`

A `String` will be produced from a string literal (any amount of characters between double quotes `"I am a string"`) or an expression that returns a `String`. `String`s are held in C++ as `std::string`s, so the character encoding is the same as the encoding used in the implementation of C++ used to compiler the interpreter.

`Strings` can be added together and produced by the addition of any combination of `String`s and `Char`s, and can also be multiplied.

```
println("Hello " + "World!");   // prints Hello World!
println("Hello " * 10);         // prints Hello Hello Hello Hello Hello Hello Hello Hello Hello Hello 
```

All values in Grace can be converted to a `String` using the `String()` cast.

```
println(String(5) + String(5));     // prints 55
```

Some characters must be expressed as escape characters inside of a `Char` and/or `String` with a backslash `\` prefix. They are:

1. Tab - `'\t'`
2. Backspace - `'\b'`
3. Newline - `'\n'`
4. Carriage Return - `'\r'`
5. Backslash - `'\\'`
6. Single quote - `'\''` (necessary in `Char` literal, not `String` literal)
7. Double quote - `"\""` (necessary in `String` literal, not `Char` literal)

## `null`

`null` represents and absence of value in Grace. If a variable is declared but not assigned, its default value will be `null`. `null` can also be assigned to a variable when needed.

```
var x;
println(x);     // prints 'null'

println(x * 5); // error - cannot perform any binary operations with null
```