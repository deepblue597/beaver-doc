# Drift detection

For detecting the phenomenon of drift in the data, two datasets were used: artificial data generated with the following code

```
rng = random.Random(12345)
dataset = rng.choices([0, 1], k=1000) + rng.choices(range(4, 8), k=1000)
```

and the real-world dataset "Electricity Data from Australia"

## Artificial Data

For the artificial data, three drift detection models were developed: ADWIN, KSWIN, and PageHinkley.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'electricityDrift'
        auto_offset_reset = "earliest"
}


algorithm <ADWIN> adwin

algorithm <PageHinkley> hinkley

algorithm <KSWIN > kswin


data drift {

    input_topic = "drift"

}

pipeline adwinPipeline {
    output_topic = 'adwinPipeline'
    data = drift
    algorithm = adwin

}

pipeline hinkleyPipeline {
    output_topic = 'hinkleyPipeline'
    data = drift
    algorithm = hinkley

}

pipeline kswinPipeline {
    output_topic = 'kswinPipeline'
    data = drift
    algorithm = kswin

}
```

![drift-elec](/img/drift-elec.dot.png)

## Electricity Data from Australia

For the electricity dataset, a model was developed using a HoeffdingTreeClassifier in combination with the DDM (Drift Detection Method) drift detector, via the DriftRetrainingClassifier wrapper. The metric used to evaluate the model's performance was accuracy.

```
connector {
        bootstrap_servers = "localhost:39092"
        security_protocol = "plaintext"
        consumer_group = 'electricityDrift'
        auto_offset_reset = "earliest"
}


algorithm <DDM> ddm

algorithm <HoeffdingTreeClassifier> hoeffTree

algorithm <DriftRetrainingClassifier > driftRetrain
    params:
        model=hoeffTree,
        drift_detector=ddm

metric <Accuracy> acc

data driftAustralia {

    input_topic = "Australia"
    features:
        target_feature = class

}

pipeline driftRetrainPipeline {
    output_topic = 'driftRetrainPipeline'
    data = driftAustralia
    algorithm = driftRetrain
    metrics = acc

}
```

![australia](/img/australiaDrift.dot.png)
