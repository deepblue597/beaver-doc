# Model Modules

Entities of type ModelModules define the modules of the River library that correspond to specific categories of algorithms.
Each ModelModule includes a variable `name` of type ModelNames, which contains the names of the allowed classes belonging to that particular module.
During the generation of the final Python code, ModelModules are used to automatically import the corresponding packages with import statements, ensuring the correct composition of the pipeline.
