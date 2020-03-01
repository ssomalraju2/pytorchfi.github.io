---
layout: default
title: Initializing
parent: PyTorchFI.Core
grand_parent: Using PyTorchFI
nav_order: 2
permalink: /core/init
---

# Initialize PyTorchFI.Core

PyTorchFI.Core must be initialized through the function call before any other functions can be called.

## Usage

PyTorchFI.Core can be initialized using the `init` function:

```python
init(model, h, w, batch_size, **kwargs)
```

### Required Parameters

1. `model`: The model in which the fault injector should be declared.

2. `h`: The height of the input to the model.

3. `w`: The width of the input to the model.

4. `batch_size`: The size of the batch for the given data.

### Optional Parameters

1. `b`: The initial batch size to run data on to acquire the output size of the model. **Default: 1**

2. `use_cuda`: A boolean whether to use CUDA or not when running the model. **Default: False**

3. `c`: The number of input channels to be used. **Default: 3**

4. `debug`: Boolean if program should print out statuses. **Default: False**

## Model Information

The model must have been trained previously and loaded with the weights, such that an inference can be run using `model(data)`. The output size of the model must also be known to the user before initialization.

## Process

Initializing PyTorchFI.Core will allow for the program to run an initial inference with the model, and collect the output size of the model. This is important because this output size is then used for verifying correct injection parameters when executing the fault injector.
