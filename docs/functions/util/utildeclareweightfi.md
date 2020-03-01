---
layout: default
title: util.declare_weight_fi
parent: PyTorchFI.Util Functions
grand_parent: Functions
nav_order: 3
permalink: /functions/util/declare_weight_fi
---

# declare_weight_fi(\*\*kwargs)

Will a declare a fault injection within the model's pretrained weights. This is stored internally, and can be changed by recalling the function with a new set of parameters.

## Parameters

1. `index`: The index of the feature in the model for which to include a weight injector.

2. `min_value`: The minimum value of the injected weight.

3. `max_value`: The maximum value of the injected weight.

## Return

None.
