# JDON
* [Overview](#overview)
* [Syntax](#syntax)
  * [Non-Functional](#non-functional)
    * [Comments](#comments)
      * [Hash](#hash)
      * [Double Slash](#double-slash)
      * [Slash Star](#slash-star)
      * [HTML](#html)
    * [Spacing](#spacing)
      * [White Space](#white-space)
      * [Blue Space](#blue-space)
      * [Green Space](#green-space)
  * [Functional](#functional)
    * [Paths](#paths)
    * [Variables](#variables)
      * [Environment Variables](#environment-variables)
      * [Local Variables](#local-variables)
    * [Assignments](#assignments)
    * [Expressions](#expressions)
      * [Unary Operators](#unary-operators)
        * [Boolean Not](#boolean-not)
      * [Binary Operators](#binary-operators)
        * [Addition](#addition)
        * [Subtraction](#subtraction)
        * [Multiplication](#multiplication)
        * [Division](#division)
        * [Modulus](#modulus)
        * [Boolean And](#boolean-and)
        * [Boolean Or](#boolean-or)
        * [Boolean Xor](#boolean-xor)
    * [Concatenation](#concatenation)
    * [Includes](#includes)
  * [Elements](#elements)
    * [Boolean](#boolean)
    * [Numeric](#numeric)
      * [Integer](#integer)
      * [Float](#float)
    * [Strings](#strings)
      * [Single Quote](#single-quote)
      * [Double Quote](#double-quote)
      * [Triple Quote](#triple-quote)
      * [Sextuple Quote](#sextuple-quote)
      * [Unquoted](#unquoted)
    * [Containers](#containers)
      * [Arrays](#arrays)
      * [Objects](#objects)

# Overview

JDON is a blend of flexible and dynamic configuration languages.  It reduces to a JSON structure.

# Syntax


## Non-Functional

### Comments

#### Hash

Hash comments begin with a # character and continue until the end of the line.  They may begin at the beginning of the line or following line content.

```
# This is a hash comment
```

#### Double Slash

Double slash comments begin with two / characters and continue until the end of the line.  They may begin at the beginning of the line or following line content.

```
// This is a double slash comment
```

#### Slash Star

Slash star comments begin with a /* and end with a */.  They may span multiple lines and may begin at the beginning of a line or within content.

```
/* This is a slash star comment
it may span multiple lines */
```

#### HTML

HTML comments begin with a &lt;!-- and end with a --&gt;.  They may span multiple lines and may begin at the beginning of a line or within content.

```
<!-- This is a slash star comment
it may span multiple lines -->
```

### Spacing

#### White Space

White space includes one or more space, tab, newline or carriage return characters.

#### Blue Space

Blue space includes any white space or comments.

#### Green Space

Green space includes spaces, tabs and until-end-of-line comments (hash and double slash).

## Functional

### Paths

Paths define relative or absolute endpoints in the document structure.  They can be applied to object keys and variables.  Paths are in the form:

```
[start designation]element[.element]+
```

If a start designation is not provided, the path is relative to the current container.  Start designations may be one of:
- ~ indicates the root of the document
- . indicates the current container
- .. indicates the parent container, additional . will reference each successive parent

### Variables

#### Environment Variables

Environment variables are defined as a path preceded by an at sign (@).  Environment variables read from the running process' environment.

Examples
```
@PATH
```

#### Local Variables

Local variables are defined as a path preceded by a dollar sign ($).  As assignments, the path must end with a named value under a valid container.  As references, the path may point to either a variable or element.  If both exist, priority is given to the variable.  When referenced, variables assume the type they are evaluated to.

Examples
```
$local_var        // references a the local variable named 'local_var'
$~root_var        // references a root variable named 'root_var'
$~0.[field_name]  // references a variable named 'field_name] under the first element under the root evel array
```

### Assignments

Assigns a value to a variable.

Definition
```
$VARPATH = value
```

Value may be any element, variable or expression.

Examples
```
$~var = 1 + 1
```

### Expressions

#### Unary Operators

##### Boolean Not

Type | Operation | Notes
--- |--- |--- |
Boolean | Boolean Not | True if bool is false
Numeric | Boolean Not | True if number is 0
String | isEmpty | True if the string length is 0
Array | isEmpty | True if the array is empty
Object | isEmpty | True if the object is empty

#### Binary Operators

##### Addition

Addition operator is a + character and supports the following operations:

Left Type | Right Type | Operation | Notes
--- |--- |--- |--- |
Boolean | Boolean | Boolean And | -
Boolean | Numeric | Boolean And | Number converted to boolean, 0 is false, non-zero is true
Boolean | String | String Concatenation | Boolean converted to string, false or true
Boolean | Array | Array Prepend | -
Boolean | Object | - | Operation not allowed
Numeric | Boolean | Boolean And | Number converted to boolean, 0 is false, non-zero is true
Numeric | Numeric | Arithmetic Add | -
Numeric | String | String Concatenation | Number converted to string
Numeric | Array | Array Prepend | -
Numeric | Object | - | Operation not allowed
String | Boolean | String Concatenation | Boolean converted to string, false or true
String | Numeric | String Concatenation | Number converted to string
String | String | String Concatenation | -
String | Array | Array Prepend | -
String | Object | - | Operation not allowed
Array | Boolean | Array Append | -
Array | Numeric | Array Append | -
Array | String | Array Append | -
Array | Array | Array Concatenation | -
Array | Object | Array Append | -
Object | Boolean | - | Operation not allowed
Object | Numeric | - | Operation not allowed
Object | String | - | Operation not allowed
Object | Array | Array Prepend | -
Object | Object | Object Concatenation | -

```
true + false          // boolean false
true + 1              // boolean true
1 + 1                 // numeric 2
foo + bar             // string foobar
[ ] + 1               // [ 1 ]
[ 1 ] + [ 2 ]         // [ 1, 2 ]
{ a: b } + { c: d }   // { a: b, c: d }
```

##### Subtraction

Subtraction operator is a - character and supports the following operations:

Left Type | Right Type | Operation | Notes
--- |--- |--- |--- |
Boolean | Boolean | - | Operation not allowed
Boolean | Numeric | - | Operation not allowed
Boolean | String | - | Operation not allowed
Boolean | Array | - | Operation not allowed
Boolean | Object | - | Operation not allowed
Numeric | Boolean | - | Operation not allowed
Numeric | Numeric | Arithmetic Subtract | -
Numeric | String | - |  Operation not allowed
Numeric | Array | - |  Operation not allowed
Numeric | Object | - | Operation not allowed
String | Boolean | - |  Operation not allowed
String | Numeric | - |  Operation not allowed
String | String | Substring Deletion | Remove all instances of substring
String | Array | - |  Operation not allowed
String | Object | - | Operation not allowed
Array | Boolean | Array Deletion | Remove all items in the array that match boolean
Array | Numeric | Array Deletion | Remove all items in the array that match number
Array | String | Array Deletion | Remove all items in the array that match string
Array | Array | Array Difference | Everything in the left array which is not in the right
Array | Object | Array Deletion | Remove all items in array that match object
Object | Boolean | - | Operation not allowed
Object | Numeric | - | Operation not allowed
Object | String | - | Operation not allowed
Object | Array | - | Operation not allowed
Object | Object | Object Difference | -

```
2 - 1                    // 1
foobar - foo             // bar
[ 1, 2, 3 ] - 2          // [ 1, 3 ]
[ 1, 2, 3 ] - [ 1, 3 ]   // [ 2 ]
{ a: b, c: d } - { c: d} // { a: b}
```

##### Multiplication

##### Division

##### Modulus

##### Boolean And

##### Boolean Or

##### Boolean Xor

### Concatenation

### Includes

```
include(PATH, [root=ROOT_PATH])
```

Include additional JDON content from file.  Paths may be any valid quoted string and reference locally accessible files on disk or via http.  If no root is given, relative paths are considered to be relative to the parent file.

```
include("examples/include.jdon", root="https://jdon.jimmyver.se/")
```

## Elements

### Boolean

Definition
```
0|1|false|true|no|yes
```
All characters are case-insensitive

Examples
```
0     # boolean false
1     # boolean true
false # boolean false
true  # boolean true
no    # boolean false
yes   # boolean true
```

### Numeric

#### Integer
Definition
```
[0-9]+|0b[01]+|0o[0-7]+|0x[0-9a-fA-F]+
```

Examples
```
100
0b1100100
0o144
0x64
```
#### Float
Definition
```
[0-9]+\.[0-9]+
```
Examples
```
3.14159
```
### Strings

#### Single Quote

Single quoted strings are strings which start and end with one single quote character.  They may not span multiple lines and may not contain variables, $ is treated literally.

```
' This is a single quoted string '
```

#### Double Quote

Double quoted strings are strings which start and end with one double quote character.  They may not span multiple lines but may contain variables.

```
" This is a single quoted string which may contain a $variable "
```

#### Triple Quote

Triple qouted strings are strings which start and end with three single quote characters.  They may span multiple lines but may not contain variables, $ is treated literally.

```
'''
This is a triple quoted string
'''
```

#### Sextuple Quote

Sextuple quoted strings are strings which start and end with three double quote characters.  They may span multiple lines and may contain variables.

```
"""
This is a sextuple quoted string which may contain a $variable
"""
```

#### Unquoted

An unquoted string is a set of characters which cannot include any of the following
```
=
#
,
[ or ]
{ or }
+ or -
* or /
!
$
"
'
newline characters (\r \n)
```

Examples
```
this is an unquoted string.
this is another unquoted string.
```

### Containers

#### Arrays

Arrays are sets of elements separated by a valid separator.  All elements are valid array members, including other arrays.  Arrays must be enclosed in brackets [ ], except if the array appears as the root level element.  Valid separators are commas (,) and end-of-line characters (\r \n).

Examples
```
[ 1, 2, 3 ]

[
  1
  2
  3
]
```

#### Objects

Objects are sets of key/value pairs separated by a valid separator.  Keys may be any valid [path](#path) and values may be any valid element, including other objects.  Objects must be enclosed in braces { }, except if the object appears as the root level element.  Valid pair separators are equals (=) and colons (:).  Valid member separators are commas (,) and end-of-line characters (\r \n).

Examples
```
{ a: b, c: d }

{
  a = b
  c = d
}
```
