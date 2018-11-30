---
title: Spark and Scala
date: 2018-06-02 10:06:26
tags: [Spark, Scala]
---
# Spark


### Initializing Spark in Java

```
import org.apache.spark.SparkConf
import org.apache.spark.SparkContext
import org.apache.spark.SparkContext._
val conf = new SparkConf().setMaster("local").setAppName("My App")
val sc = new SparkContext(conf)
```


### Definiation
RDD: resilient distributed dataset 
sc: SparkContext

# Scala Syntax

__To install__: The repository is too old(2.9.2) use the command

wget www.scala-lang.org/files/archive/scala-2.11.7.deb
sudo dpkg -i scala-2.11.7.deb

**syntax**: val <identifier>[: <type>] = <data>  //[: type] is optional

REPL: scala Interpreter


* val for value is immutable
* var for variable is mutable

since value is immutable we perfer value to prevent unexpected change


### numeric
Scala does not allow automatic conversion from higher ranked types to lower ranked types. You can choose to manually convert between types using the *toType* methods available on all numeric types.


### String

A multiline String can be created using triple-quotes. Multiline strings are literal, and
so do not recognize the use of backslashes as the start of special characters:



You will need the optional braces if you have any nonword characters in your reference (such as a calculation), or if your reference can’t be distinguished from the surrounding text: ${<value name>} or ${<value name> * num}

### Regular expression

***Syntax***: val <Regex value>(<identifier>) = <input string>
* The value will be stored in identifier
* convert a string to a regular ex‐ pression type by invoking its r operator.

We’ll use multiline strings to store our regular expression pattern, because they are literal and allow us to write a backslash without a second, escaping backslash:


### Type
* Any is the root of scala type
* ref is access via memory reference
* Nothing is a subtype of every other type and exists to provide a compatible return type for operations that significantly affect a program’s flow. 
* Null, a subtype of all AnyRef types that exists to provide a type for the keyword null. such that the variable does not point to any string instance in memory.
* & and | will always check the second variable or expression. && and || are lazy they only check the first one. If the first one is sufficient, it stops.
* Scala does not support automatic conversion of other types to Booleans
* Unit type is used to describe the function doesnt return anything. Like the void in C++ && Java. Unit literally equal to () Unit = ()


#### Type Operation

**Syntax**: val.<Type Operation>

__perfer to<type> avoid asInstanceof[<type>]__
* asInstanceOf[<type>]: change to type 
* getClass: return type of value
* isInstanceOf: return true if the value has the given type
* hashCode: Returns the hash code of the value, useful for hash-based collections
* to<type>: Conversion functions to convert a value to a compatible value.
* toString: Renders the value to aString.



### Tuple
__Syntax__: ( <value 1>, <value 2>[, <value 3>...] )

access an individual element from a tuple by its 1-based index (e.g., where the first element is 1, second is 2, etc.):

_example_: tuplename._1

An alternate form of creating a 2-sized tuple is with the relation operator (->). This is a popular shortcut for representing key-value pairs in tuples:

scala> val red = "red" -> "0xff0000"   
red: (String, String) = (red,0xff0000)


### Expression

#### Syntax   
__if-else__
```
if (<Boolean expression>) <expression>
else <expression>
```
__match__ 
```
<expression> match {
      case <pattern match> => <expression>
      [case...]
}
```

__Matching with Wildcard Patterns__
```
 case <identifier> => <one or more expressions>
```
__A Wildcard Operator Pattern__
```
case _ => <one or more expressions>
```

__A Pattern Guard__
```
    case <pattern> if <Boolean expression> => <one or more expressions>
```


__Specifying a Pattern Variable__
```
    case <identifier>: <type> => <one or more expressions>
```


## Loops

### Range and For-Loop
```
//range
<starting integer> [to|until] <ending integer> [by increment]

//for   the yield keyword to con‐ vert the entire loop into an expression that returns the collection:
for (<identifier> <- <iterator>) [yield] [<expression>]

//An Iterator Guard
for (<identifier> <- <iterator> if <Boolean expression>) ...
```

## Value Binding

Syntax: 
```
// Value Binding in For-Loops
for (<identifier> <- <iterator>; <identifier> = <expression>) ...

```
## While
Syntax: 
```
// A While Loop
while (<Boolean expression>) statement
```

## Function

Syntax: 
```
Defining an Input-less Function
    def <identifier> = <expression>

Defining a Function with a Return Type
    def <identifier>: <type> = <expression>
    
Defining a Function
    def <identifier>(<identifier>: <type>[, ... ]): <type> = <expression>
    
Defining a Function with Empty Parentheses
    def <identifier>()[: <type>] = <expression>
    
Invoking a Function with an Expression Block
    <function identifier> <expression block>

Specifying a Parameter by Name
<function name>(<parameter> = <value>)

Specifying a Default Value for a Function Parameter
def <identifier>(<identifier>: <type> = <value>): <type>

Defining a Function’s Type Parameters
def <function-name>[type-name](parameter-name>: <type-name>): <type-name>...

 A Function Type
    ([<type>, ...]) => <type>
    
Assigning a Function with the Wildcard Operator
    val <identifier> = <function name> _

Writing a Function Literal    
([<identifier>: <type>, ... ]) => <expression>

Specifying a By-Name Parameter
    <identifier>: => <type>

```