# Params

Each parameter entity has 2 parameters :

- `name` -> the name of the variable (optional)
- `value` -> it is an entity of type ParamValue. ParamValue can be of the below types
  - TypeRef
  - NUMBER
  - STRING
  - BOOL
  - Tuple
  - List
  - Dict
  - ModelRef

Below there are explanations for some of the more complex ones.

## List

A List defines a sequence of parameter values, enclosed in square brackets `[ ]`.  
The elements of the list are of type `ParamValue` and are separated by commas.  
It is used to specify multiple values for a single parameter.

---

## Tuple

A Tuple defines a fixed sequence of values, enclosed in parentheses `( )`,  
where the elements are of type `ParamValue` and separated by commas.  
Tuples are typically used when you want to declare constant, immutable sets of values.

---

## Dict

A Dict (dictionary) represents collections of key-value pairs, enclosed in curly braces `{ }`.  
Each pair consists of a name (string) and the corresponding value of type `ParamValue`,  
separated by a colon, with pairs separated by commas.  
Dicts allow grouping of parameters with explicit names.

---

## DictItem

A DictItem represents an individual key-value pair within a Dict.  
The key is always a string and the value is of type `ParamValue`.

---

## ModelRef

ModelRef allows referencing an already defined Model within a parameter.  
Instead of defining the entire model from scratch, you refer to the model's name (`name`).

---

## TypeRef

TypeRef is a custom variable to be able to define ID inside the parameter values.
