---
layout: default
title: Declaring A Fault Injector
parent: PyTorchFI.Core
grand_parent: Using PyTorchFI
nav_order: 3
permalink: /core/declare-fi
---

# Declaring a Fault Injector with PyTorchFI.Core

A `fault_injector` class may be intaintated by passing the model desired for testing. 

```python
import torch
from pytorchfi import core
torch.random.manual_seed(5)
image = torch.rand((10, 3, 224, 224))
h = 224
w = 224
batch_size = 1
torch.no_grad()

# load model
model = models.resnet50(pretrained=True)
# Instantiate fault injector class
fi_model = core.fault_injection(model, h, w, batch_size)
```

## Injection Locations

### Neuron Injection
This injection allows for dynamic insertion of values after the specified 
layer. 

#### Single Injection

```python
kwargs = {'value': 310810, 'layer_num': 3, 'c': 1, 'batch': 0, 'layer_type':'ReLu'}
fi_model.declare_neuron_fi(**kwargs)
```

#### Multi-Injection

```python
kwargs = {'value': (310810,20910,-101), 'layer_num': (1,2,6), 'c': (1,1,(3,20,20)), 'batch': (0,0,12)}
fi_model.declare_neuron_fi(**kwargs)
```

### Weight Injection
This injection allows for inertion of persistent modifications to the designated weights. 

```python
kwargs = {'value': 310810, 'layer_num': 3, 'index': 1, 'batch': 0, 'layer_type':'ReLu'}
fi_model.declare_weight_fi(**kwargs)
```


## Injection Utilities

### Random Injection

Injection utils that allow for inserting random injections
```python
from pytorchfi import util
fi.model.util.random_weight_inj(self, min_val=-1, max_val=1):
```
Samples a value from the uniform distribution between `min_val` and `max_val` and injects this value
into the weights of a randomly selected layer. 


If a random injection **in every batch** is desired, then the only parameters that can be given to the function is `value`, `min_value`, and `max_value`.

#### Function Injection

A function can be given that will run a custom injection. The function must follow the forward-hook specifications of PyTorchFI. For example, a injection function could be

```python
def set_zero(self, input, output):
    output = torch.IntTensor(output.size()).zero_()
```

which will zero every output tensor.


#### Parameters

**All parameters given are optional**. As specified above, this will result in a random injection for every batch.

1. `conv_num`: The convolution in which the fault injector should run.

2. `batch`: The batch in which the fault injector should run.

3. `c`: The channel number.

4. `w`: The width number.

5. `h`: The height number.

6. `value`: The value that the injector should set within the tensor. If this value is given along with a range with `min_value` and `max_value`, this is the value that will be injected.

7. `min_value`: The minimum value of the value to be injected. Only used if no `value` parameter is given. **Default: -500**

8. `max_value`: The maximum value of the value to be injected. Only used if no `value` parameter is given. **Default: 500**

### Weight Injection

Will include an injection within the weights of the model.

#### Parameters

**All parameters are required**.

1. `index`: The index of the feature in the model for which to include a weight injector.

2. `min_value`: The minimum value of the injected weight.

3. `max_value`: The maximum value of the injected weight.

#### Usage

```python
model = core.declare_weight_fi(0, -1e-3, 1e-3)
```

## Model Returned

The model returned **is a copy** of the original model PyTorchFI.Core Fault Injection was initialized with. This implementation was specifically chosen such that a variety of fault injections could be declared with only a single initialization.

The model injection values are also verified to be valid, so that there will be no errors when running the model on data.
