---
layout: default
title: Utility Functions
parent: PyTorchFI.Util
grand_parent: Using PyTorchFI
nav_order: 4
permalink: /util/utility
---

# Utility of PyTorchFI.Util

## Available Functions

### compare_golden()

`compare_golden()` will run the given input data on the original model, and then also on the model with the declared fault injector. It will then return an array of the probability for the identified classes for both results, where `result[0]` corresponds to the golden output, and `result[1]` corresponds to the corrupted output.

### time_model()

`time_model()` will return how long it took the model to run with the given input.

### random_batch_fi_gen(conv_number, fmap_number, H_size, W_size, min_value, max_value)

This function will generate a random set of fault injections within the given PyTorchFI instance. It will generate an injection for each batch at a random location in the tensor, within the range of `min_value` and `max_value` and return a list for injections.
