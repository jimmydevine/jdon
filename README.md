# jdon
* [Overview](#overview)
* [Syntax](#syntax)
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
  * [Functional](#functional)
    * [Paths](#paths)
    * [Variables](#variables)
      * [Environment Variables](#environment-variables)
      * [Local Variables](#local-variables)
    * [Assignments](#assignments)
    * [Expressions](#expressions)
      * [Unary Operators](#unary-operators)
        * [Not](#not)
      * [Binary Operators](#binary-operators)
        * [Add](#add)
        * [Subtract](#subtract)
        * [Multiply](#multiply)
        * [Divide](#divide)
        * [Mod](#mod)
        * [And](#and)
        * [Or](#or)
        * [Xor](#xor)
    * [Concatenation](#concatenation)
    * [Includes](#includes)
  * [Non-Functional](#non-functional)
    * [Spacing](#spacing)
    * [Comments](#comments)
      * [Hash](#hash)
      * [Double Slash](#doubler-slash)
      * [Slash Star](#slash-star)
      * [HTML](#html)


# Overview

# Syntax

## Elements

### Boolean

### Numeric

#### Integer

#### Float

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

### Containers

#### Arrays

#### Objects

## Functional

### Paths

### Variables

#### Environment Variables

#### Local Variables

### Assignments

### Expressions

#### Unary Operators

##### Not

#### Binary Operators

##### Add

##### Subtract

##### Multiply

##### Divide

##### Mod

##### And

##### Or

##### Xor

### Concatenation

### Includes

## Non-Functional

### Spacing

### Comments

#### Hash

#### Double Slash

#### Slash Star

#### HTML
