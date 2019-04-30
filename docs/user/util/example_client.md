---
layout: default
title: Example Util Client
parent: PyTorchFI.Util
grand_parent: Using PyTorchFI
nav_order: 5
---

# PyTorchFI.Util Example Client

The following is an example client on how to use the full functionality of PyTorchFI.Util.

```python
from src import PyTorchFI_Source_Util

if __name__ == "__main__":
    PyTorchFI_Source_Util.init(model, input)
    PyTorchFI_Source_Util.declare_fi(
        conv_num=2, batch=0, x=2, y=1, z=1, value=10000000000000
    )

    results = PyTorchFI_Source_Util.compare_golden()
    print("Expected vs Corrupted")
    for index, predicted_val in enumerate(results[0]):
        print(
            "%s vs. %s"
            % (CIFAR10_CLASSES[predicted_val], CIFAR10_CLASSES[results[1][index]])
        )
```

## Predefined Variables

1. `model`: model with pretrained weights loaded.

2. `input`: the dataset to be run with the model.

## Initializing PyTorchFI.Core

`pytorchfi.init(model, input)` initializes the model with a given data set.

## Specified Fault Injector

```python
model = pytorchfi.declare_fi(
        conv_num=2, batch=0, c=2, w=1, h=1, value=10000000000000
    )
```

This will initialize fault injector mode within the Util program, and store the fault injection for future injections.

## Comparing Output

Once we have initialized the fault injection we want to run, we can get an array with the results of the fault injector to that of the golden output.

```python
results = PyTorchFI_Source_Util.compare_golden()
```
