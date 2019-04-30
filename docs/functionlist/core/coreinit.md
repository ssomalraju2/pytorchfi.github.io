---
layout: default
title: core.init
parent: PyTorchFI.Core Functions
grand_parent: Function List
nav_order: 1
---

# init(model, h, w, batch_size, \*\*kwargs)

Will initialize PyTorchFi with a model and a given data set. These are both stored through the scope of the module usage within the program, and are specifically used whenever running the fault injection.

## Required Parameters

1. `model`: The model in which the fault injector should be declared. The model must have been trained previously and loaded with the weights, such that an inference can be run using `model(data)`. The output size of the model must also be known to the user before initialization.

2. `h`: The height of the input to the model.

3. `w`: The width of the input to the model.

4. `batch_size`: The size of the batch for the given data.

## Optional Parameters

1. `b`: The initial batch size to run data on to acquire the output size of the model. **Default: 1**

2. `use_cuda`: A boolean whether to use CUDA or not when running the model. **Default: False**

3. `c`: The number of input channels to be used. **Default: 3**

4. `debug`: Boolean if program should print out statuses. **Default: False**

## Return

None.
