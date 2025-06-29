# Ensemble Example

This example works on the Phishing dataset. The goal is to predict whether a sample is phishing or not (binary classification) using an ensemble method. We will use AdaBoost with a Hoeffding Tree base classifier.

## Models

We will use the following models and components:

- **HoeffdingTreeClassifier** as the base estimator for AdaBoost.
- **AdaBoostClassifier** as the ensemble method.

We will also use the following metric for evaluation:

- **LogLoss**

## Preprocessing

No explicit preprocessing is defined in this example, as the Hoeffding Tree can handle raw features directly. If your data requires preprocessing, you can add preprocessors as needed.

## Beaver File Structure

Let's see how we would write the beaver file:

### Connector

We start by defining the connector, specifying the Kafka bootstrap servers and security protocol.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'ensemble'
        auto_offset_reset = "earliest"
}
```

### Models

We define the base classifier and the AdaBoost ensemble:

```
algorithm <HoeffdingTreeClassifier> hoeff
    params:
        split_criterion='gini',
        delta=1e-5,
        grace_period=2000

algorithm <AdaBoostClassifier> adaboost
    params:
        model=hoeff,
        n_models=5,
        seed=42
```

### Metric

We define the evaluation metric:

```
metric <LogLoss> logloss
```

### Data

We define the data source and specify the target feature:

```
data Phishing {
    input_topic = "Phishing"
    features:
        target_feature = is_phishing
}
```

### Pipeline

Finally, we define the pipeline that brings everything together:

```
pipeline adaboostPipeline {
    output_topic = 'adaboostPipeline'
    data = Phishing
    algorithm = adaboost
    metrics = logloss
}
```

And that's it! This setup allows you to use AdaBoost with Hoeffding Trees to improve classification performance on the Phishing dataset by

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'ensemble'
        auto_offset_reset = "earliest"
}

algorithm <HoeffdingTreeClassifier> hoeff
    params:
        split_criterion='gini',
        delta=1e-5,
        grace_period=2000



algorithm <AdaBoostClassifier> adaboost
    params:
        model=hoeff,
        n_models=5,
        seed=42



metric <LogLoss> logloss

data Phishing {

    input_topic = "Phishing"
    features:
        target_feature = is_phishing
}

pipeline adaboostPipeline {
    output_topic = 'adaboostPipeline'
    data = Phishing
    algorithm = adaboost
    metrics = logloss

}
```
