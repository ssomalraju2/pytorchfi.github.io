---
layout: default
title: Declaring A Fault Injector
parent: PyTorchFI.Core
grand_parent: Using PyTorchFI
nav_order: 3
permalink: /core/declare-fi
---

# Declaring a Fault Injector with PyTorchFI.Core

There are many ways to declare a fault injection within PyTorchFI.

## Types of Injections

### Neuron Injection

Will include an injection within the neurons of the model.

#### Specific Injection

If an injection at a specific location with a specific value is desired, then all parameters should be given. **PyTorchFI.Core does not save previous values from injections**, so if all parameters are not given, there will be an injection value error.

#### Random Injection

If a random injection **in every batch** is desired, then the only parameters that can be given to the function is `value`, `min_value`, and `max_value`.

#### Function Injection

A function can be given that will run a custom injection. The function must follow the forward-hook specifications of PyTorchFI. For example, a injection function could be

```python
def set_zero(self, input, output):
    output = torch.IntTensor(output.size()).zero_()
```

which will zero every output tensor.

#### Number of Injections

- A single injection can be declared by passing a single value in for each of the parameters.
- Multiple injections can be declared by passing a list of values for each of the parameters. Note that each list must be the same size. The fault injection will be declared using the corresponding values by index.

#### Usage

```python
def declare_neuron_fi(**kwargs):
```

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
model = pytorchfi.declare_weight_fi(0, -1e-3, 1e-3)
```

## Model Returned

The model returned **is a copy** of the original model PyTorchFI.Core was initialized with. This implementation was specifically chosen such that a variety of fault injections could be declared with only a single initialization.

The model injection values are also verified to be valid, so that there will be no errors when running the model on data.
