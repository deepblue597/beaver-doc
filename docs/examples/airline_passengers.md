# Airline Passengers Forecasting

This example demonstrates how to perform time series forecasting on the Airline Passengers dataset using the Holt-Winters method.

## Models

We use the following model and metric:

- **HoltWinters:** A triple exponential smoothing model suitable for time series with trend and seasonality. Configured with:
  - `alpha=0.3`
  - `beta=0.1`
  - `gamma=0.6`
  - `seasonality=12`
  - `multiplicative=True`
- **MAE (Mean Absolute Error):** Used to evaluate forecasting accuracy.

## Beaver File Structure

Let's see how we would write the beaver file:

### Connector

We start by defining the connector, specifying the Kafka bootstrap servers and security protocol.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'time_series_models'
        auto_offset_reset = "earliest"
}
```

### Model

We define the Holt-Winters forecasting algorithm:

```
algorithm <HoltWinters> winters
    params:
        alpha=0.3,
        beta=0.1,
        gamma=0.6,
        seasonality=12,
        multiplicative=True
```

### Metric

We define the evaluation metric:

```
metric <MAE> mae
```

### Data

We define the data source and specify the target feature:

```
data AirlinePassengers {

    input_topic = "AirlinePassengers"
    features:
        target_feature = passengers

}
```

### Pipeline

Finally, we define the pipeline that brings everything together:

```
pipeline wintersPipeline {
    output_topic = 'wintersPipeline'
    data = AirlinePassengers
    algorithm = winters
    metrics = mae
}
```

This configuration enables robust time series forecasting on the Airline Passengers dataset, making it easy to evaluate the performance of the Holt-Winters method for seasonal data.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'time_series_models'
        auto_offset_reset = "earliest"
}

algorithm <HoltWinters> winters
    params:
        alpha=0.3,
        beta=0.1,
        gamma=0.6,
        seasonality=12,
        multiplicative=True

metric <MAE> mae

data AirlinePassengers {

    input_topic = "AirlinePassengers"
    features:
        target_feature = passengers

}


pipeline wintersPipeline {
    output_topic = 'wintersPipeline'
    data = AirlinePassengers
    algorithm = winters
    metrics = mae
}
```
