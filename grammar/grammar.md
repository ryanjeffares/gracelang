# Grammar

This file contains the grammar for the Grace language, presented in [EBNF](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)

# Syntax Grammar

```ebnf

program = { declaration } EOF ;

```

## Declarations

```ebnf

declaration = classDecl
			| funcDecl
			| varDecl
			| finalDecl
			| statement ;

classDecl = "class" IDENTIFIER ":" { function } "end" ;

funcDecl = "func" [ "export" ] IDENTIFIER "(" [ [ "final" ] IDENTIFIER [ { "," [ "final" ] IDENTIFIER } ] ] ")" ":" block "end" ;

varDecl = "var" IDENTIFIER [ "=" expression ] ";" ;

finalDecl = "final" IDENTIFIER "=" expression ";" ;

```

## Statements

```ebnf

statement = exprStmt
		  | forStmt
		  | ifStmt
		  | printStmt
		  | printLnStmt
		  | returnStmt
		  | whileStmt
			| tryStmt
			| throwStmt
			| assertStmt
			| breakStmt
			| continueStmt
		  | block ;

exprStmt = expression ";" ;

forStmt = "for" IDENTIFIER "in" expression ":"
		block
		"end" ;

ifStmt = "if" expression ":"
		block
		[ { "else" "if" expression ":" block } ]
		[ "else" ":" block ]
		"end" ;

printStmt = "print" "(" expression ")" ";" ;

printLnStmt = "println" "(" expression ")" ";" ;

returnStmt = "return" [ expression ] ";" ;

whileStmt = "while" expression ":" 
			block 
			"end" ;

tryStmt = "try" ":"
			block
			"catch" IDENTIFIER ":"
			block
			"end" ;

throwStmt = "throw" "(" expression ")" ;

assertStmt = "assert" "(" expression [ "," expression ] ")" ;

breakStmt = "break" ;

continueStmt = "continue" ;

block = { declaration - funcDecl, classDecl } ;

```

## Expressions

```ebnf

expression = assignment | logic_or ;

assignment = [ { call "." } ] IDENTIFIER "=" logic_or ;

logic_or = logic_and [ { "or" logic_and } ] ;

logic_and = equality [ { "and" equality } ] ;

equality = comparison [ { ( "!=" | "==" ) comparison } ] ;

comparison = term [ { ( ">" | ">=" | "<" | "<=" ) term } ] ;

term = factor [ { ( "-" | "+" ) factor } ] ;

factor = unary [ { ( "/" | "*" ) unary } ] ;

unary = [ ( "!" | "-" ) ] unary | call ;

call = primary [ { "(" [ expression [ { "," expression } ] ] ")" | "." IDENTIFIER } ] ;

primary = "true" | "false" | "this" | instanceof | isobject | cast
		| NUMBER | STRING | IDENTIFIER | "(" expression ")"
		| LIST | DICT ;

instanceof = "instanceof" "(" expression "," TYPE ")" ;

isobject = "isobject" "(" expression ")" ;

cast = TYPE "(" expression ")" ;

```

## Lexical Grammar

```ebnf

NUMBER = INTEGER | FLOAT ;

INTEGER = { DIGIT } | "0" ( "b" | "B") { "0" | "1" } | "0" ( "x" | "X" ) { "a" ... "f" | "A" ... "F" | "0" ... "9" };

FLOAT = { DIGIT } "." { DIGIT } ;

STRING = '"' any char '"';

IDENTIFIER = ALPHA, { ALPHA | DIGIT } ;

ALPHA = "a" ... "z" | "A" ... "Z" | "_" ;

DIGIT = "0" ... "9" ;

TYPE = "int" | "float" | "bool" | "string" | "char" ;

RANGE = expression ".." expression [ "by" expression ] ;

LIST = "[" [ { expression "," } | RANGE ] "]" ;

DICT = "{" [ { expression ":" expression "," } ] "}" ;

```

## Keywords

```ebnf

keyword = "class"
		| "func"
		| "export"
		| "for"
		| "in"
		| "by"
		| "while"
		| "end"
		| "if"
		| "else"
		| "true"
		| "false"
		| "this"
		| "null"
		| "var"
		| "final"
		| "instanceof"
		| "isobject"

```
