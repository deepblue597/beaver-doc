# Model Types

Each of the seven ModelGroups categories corresponds to a ModelType, which defines the structure of the individual models belonging to each group. ModelTypes are sub-entities of the Model entity and shape the internal representation of machine learning units in the Beaver language.

This structure allows for a strict separation between the different types of models in the River library and facilitates the display of appropriate error messages in cases of incorrect syntax or improper class usage.

Each ModelType is defined with the following variables:

- `type`: The name of the River class that implements the algorithm
- `name`: The identifier given to the object in the Beaver program
- `params`: A list of parameters corresponding to the arguments of the Python class (with name and value)
