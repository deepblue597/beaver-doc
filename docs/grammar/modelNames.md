# Model Names

Entities of type ModelNames define the set of allowed names for machine learning models supported by the Beaver language.
Each value in this entity corresponds to a valid class from the River library, and is used for identifying and constructing the corresponding Python objects during the compilation phase.
By using the object cross-referencing mechanism of textX, it is ensured that the user can only use predefined and supported models.
If an invalid name is declared, a diagnostic error message is displayed.
