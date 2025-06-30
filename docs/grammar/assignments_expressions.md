# Assignment & Expression

The **Assignment** entity defines the assignment of a value to a variable. Specifically, a variable (with an identifier of type `ID`) is assigned a value resulting from the evaluation of an arithmetic expression, which follows the standard mathematical order of operations.

An **Expression** consists of one or more terms (`Term`) connected by addition or subtraction operators (`+` or `-`).  
Each term, in turn, consists of one or more factors (`Factor`), which are connected by multiplication or division operators (`*` or `/`).

Each factor may optionally have a sign (`+` or `-`) and can be either:

- a number (`NUMBER`),
- a reference to a variable (`ID`), or
- a sub-expression enclosed in parentheses, thus allowing
