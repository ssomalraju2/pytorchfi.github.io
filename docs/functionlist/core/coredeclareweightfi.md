---
layout: default
title: core.declare_weight_fi
parent: PyTorchFI.Core Functions
grand_parent: Function List
nav_order: 3
---

# declare_weight_fi(\*\*kwargs)

Will a declare a fault injection within the model's pretrained weights. This is stored internally, and can be changed by recalling the function with a new set of parameters.

## Parameters

1. `index`: The index of the feature in the model for which to include a weight injector.

2. `min_value`: The minimum value of the injected weight.

3. `max_value`: The maximum value of the injected weight.

## Return

The model with the weight fault injector.
