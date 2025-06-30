# Beaver Model

The **BeaverModel** defines the structure and key components that must be included in a Beaver language file.  
These files are saved with the `.bvr` extension. The order of elements within the file should be as follows:

1. **connector**
2. **models**
3. **data**
4. **pipelines**

This order was chosen to reflect the flow of data from one component to the next.  
Additionally, the simpler elements are defined first, while the more complex ones are placed at the end, making the file easier to organize and understand.

A visualization of the Beaver metamodel is shown below.

![pipeline](/img/pipeline.png)
