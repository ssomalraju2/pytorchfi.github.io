---
layout: default
title: util.declare_neuron_fi
parent: PyTorchFI.Util Functions
grand_parent: Function List
nav_order: 2
---

# declare_neuron_fi(\*\*kwargs)

Will a declare a fault injection within the model used for initialization. This is stored internally, and can be changed by recalling the function with a new set of parameters.

If the function is called with no parameters, then a random injection is initialized. Otherwise, **all** of the following parameters must be defined for a specific fault injector to be defined.

## Optional Parameters

1. `conv_num`: The convolution in which the fault injector should run.

2. `batch`: The batch in which the fault injector should run.

3. `c`: The channel number.

4. `w`: The width number.

5. `h`: The height number.

6. `value`: The value that the injector should set within the tensor.

## Return

None.
