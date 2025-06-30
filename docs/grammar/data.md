# Data

The **Data** entity is used to define the characteristics of the data. Specifically, the user specifies the following parameters:

1. **name:** The name of the data object defined by the user.
2. **input_topic:** The name of the repository where the data to be processed is stored.
3. **features:** The elements of the data, as described in [features](../features).
4. **preprocessors:** Reference to the name of zero or more `ProcList`.

## ProcList

Each **ProcList** is a list of references to one or more `DataModel` entities.  
DataModels include 3 types of models. Using any other type will result in an error.

Additionally, the structure of a ProcList defines the flow of data through these processors:

- Separating two or more processors with the symbol `|` tells Beaver that the data will pass sequentially from the first processor, and the output of the first will be used as the input to the second.
- Separating processors with the symbol `+` means that the data will pass through both processors in parallel.

For more information on using the `+` operator, see the River language manual, section
