---
layout: default
title: util.init
parent: PyTorchFI.Util Functions
grand_parent: Function List
nav_order: 1
---

# init(model, data, \*\*kwargs)

Will initialize PyTorchFi with a model and a given data set. These are both stored through the scope of the module usage within the program, and are specifically used whenever running the fault injection.

## Required Parameters

1. `model`: The model in which the fault injector should be declared.

2. `data`: The data to be used within the utility class.

## Optional Parameters

1. `use_cuda`: A boolean whether to use CUDA or not when running the model. **Default: False**

2. `debug`: Boolean if program should print out statuses. **Default: False**

## Return

None.
