# Pipeline

The **Pipeline** represents the overall system used for data collection and processing, algorithm training, prediction generation, metric usage, and result presentation.  
It includes the following parameters:

1. **name:** The name to be used for the pipeline.
2. **output_topic:** The Kafka topic where the generated data will be stored.
3. **data:** Reference to the `Data` entity that will be used by the pipeline.
4. **algorithm:** The algorithm that will be trained and will generate predictions.
5. **metrics:** The metrics that will be used to evaluate the algorithm and present results to the user.
