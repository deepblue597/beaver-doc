# Model Selection

This example demonstrates how to perform online model selection using a multi-armed bandit approach on the Phishing dataset.

## Models and Optimizers

We use the following models and components:

- **LogisticRegression**: Two logistic regression models, each with a different SGD optimizer:
  - `log1` uses `sgd1` (learning rate 0.0001)
  - `log2` uses `sgd2` (learning rate 0.00001)
- **BanditClassifier**: Combines multiple models and selects the best one online using a bandit policy.
- **EpsilonGreedy**: The bandit policy used to balance exploration and exploitation, with parameters for epsilon, decay, burn-in, and random seed.

We also use the following metric for evaluation:

- **Accuracy**

## Preprocessing

- **StandardScaler** is used to standardize features for the dataset.

## Beaver File Structure

Let's see how we would write the beaver file:

### Connector

We start by defining the connector, specifying the Kafka bootstrap servers and security protocol.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'model_selection_models'
        auto_offset_reset = "earliest"
}
```

### Models and Optimizers

We define the optimizers, logistic regression models, bandit policy, and the bandit classifier:

```
optimizer <SGD> sgd1
    params:
        lr= 0.0001

optimizer <SGD> sgd2
    params:
        lr= 1e-05

algorithm <LogisticRegression> log1
    params:
        optimizer =sgd1

algorithm <LogisticRegression> log2
    params:
        optimizer =sgd2

algorithm <EpsilonGreedy> epsilon
    params:
        epsilon=0.1,
        decay=0.001,
        burn_in=20,
        seed=42

algorithm <BanditClassifier> bandit
    params:
        models = [log1 , log2],
        metric = acc,
        policy = epsilon
```

### Preprocessing

We define the preprocessor:

```
preprocessor <StandardScaler> scaler
```

### Metric

We define the evaluation metric:

```
metric <Accuracy> acc
```

### Data

We define the data source and specify the target feature and preprocessor:

```
data Phishing {

    input_topic = "Phishing"
    features:
        target_feature = is_phishing
    preprocessors = scaler
}
```

### Pipeline

Finally, we define the pipeline that brings everything together:

```
pipeline banditPipeline {
    output_topic = 'banditPipeline'
    data = Phishing
    algorithm = bandit
    metrics = acc
}
```

And that's it! This setup allows you to automatically select and adapt between different models in an online fashion, optimizing performance on the Phishing dataset using a bandit-based selection strategy.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'model_selection_models'
        auto_offset_reset = "earliest"
}

optimizer <SGD> sgd1
    params:
        lr= 0.0001

optimizer <SGD> sgd2
    params:
        lr= 1e-05

algorithm <LogisticRegression> log1
    params:
        optimizer =sgd1

algorithm <LogisticRegression> log2
    params:
        optimizer =sgd2

preprocessor <StandardScaler> scaler

metric <Accuracy> acc

algorithm <EpsilonGreedy> epsilon
    params:
        epsilon=0.1,
        decay=0.001,
        burn_in=20,
        seed=42


algorithm <BanditClassifier> bandit
    params:
        models = [log1 , log2],
        metric = acc,
        policy = epsilon



data Phishing {

    input_topic = "Phishing"
    features:
        target_feature = is_phishing
    preprocessors = scaler
}


pipeline banditPipeline {
    output_topic = 'banditPipeline'
    data = Phishing
    algorithm = bandit
    metrics = acc
}
```
