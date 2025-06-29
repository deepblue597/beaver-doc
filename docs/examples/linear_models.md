# Linear Models Example

This example demonstrates how to build and evaluate linear model pipelines for two different datasets: a phishing detection dataset and a Trump approval rating dataset.

## Models

We use the following models and components:

- **ALMAClassifier** for online binary classification.
- **LinearRegression** for regression tasks, with a specified learning rate for the intercept.

We also use the following metrics for evaluation:

- **Accuracy** (for classification)
- **MAE (Mean Absolute Error)** (for regression)

## Preprocessing

- **StandardScaler** is used to standardize features for both datasets.

## Beaver File Structure

Let's see how we would write the beaver file:

### Connector

We start by defining the connector, specifying the Kafka bootstrap servers and security protocol.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'linear_models'
        auto_offset_reset = "earliest"
}
```

### Models

We define the algorithms and the preprocessor:

```
algorithm <ALMAClassifier> alma

algorithm <LinearRegression> linear
    params:
        intercept_lr=0.1

preprocessor <StandardScaler> scaler
```

### Metrics

We define the evaluation metrics:

```
metric <MAE> mae
metric <Accuracy> acc
```

### Data

We define the data sources and specify the target features and preprocessors:

```
data Phishing {

    input_topic = "Phishing"
    features:
        target_feature = is_phishing
    preprocessors = scaler
}

data TrumpApproval {

    input_topic = "TrumpApproval"
    features:
        target_feature = five_thirty_eight
    preprocessors = scaler
}
```

### Pipelines

Finally, we define the pipelines that bring everything together:

```
pipeline almaPipeline {
    output_topic = 'almaPipeline'
    data = Phishing
    algorithm = alma
    metrics = acc
}

pipeline LinearRegressionPipeline {
    output_topic = 'LinearRegressionPipeline'
    data = TrumpApproval
    algorithm = linear
    metrics = mae
}
```

And that's it! This setup allows you to apply and compare linear models for both classification and regression tasks, using standardized preprocessing and appropriate evaluation metrics.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'linear_models'
        auto_offset_reset = "earliest"
}

algorithm <ALMAClassifier> alma

algorithm <LinearRegression> linear
    params:
        intercept_lr=0.1

preprocessor <StandardScaler> scaler

metric <MAE> mae
metric <Accuracy> acc

data Phishing {

    input_topic = "Phishing"
    features:
        target_feature = is_phishing
    preprocessors = scaler
}

data TrumpApproval {

    input_topic = "TrumpApproval"
    features:
        target_feature = five_thirty_eight
    preprocessors = scaler
}

pipeline almaPipeline {
    output_topic = 'almaPipeline'
    data = Phishing
    algorithm = alma
    metrics = acc
}

pipeline LinearRegressionPipeline {
    output_topic = 'LinearRegressionPipeline'
    data = TrumpApproval
    algorithm = linear
    metrics = mae
}
```
