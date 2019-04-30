---
layout: default
title: util.random_batch_fi_gen
parent: PyTorchFI.Util Functions
grand_parent: Function List
nav_order: 6
---

# random_batch_fi_gen(conv_number, fmap_number, H_size, W_size, min_value, max_value)

This function will generate a random set of fault injections within the given PyTorchFI instance. It will generate an injection for each batch at a random location in the tensor, within the range of `min_value` and `max_value` and return a list for injections.

## Optional Parameters

1. `conv_num`: The convolution in which the fault injections should be generated.

2. `fmap_number`: The batch in which the fault injections should be generated.

3. `H_size`: The size of h in the input.

4. `W_size`: The size of w in the input.

5. `min_value`: The minimum value that for any of the randomly generated fault injections.

6. `max_value`: The maximum value that for any of the randomly generated fault injections.

## Return

A list of fault injections, each index corresponding to the required index for `declare_fi` function.
