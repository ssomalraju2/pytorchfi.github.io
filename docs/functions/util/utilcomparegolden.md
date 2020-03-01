---
layout: default
title: util.compare_golden
parent: PyTorchFI.Util Functions
grand_parent: Functions
nav_order: 4
permalink: /functions/util/compare_golden
---

# def compare_golden()

This function should be called after a declared injection. It will automatically run the data on both the original model, as well as the model with the fault injector. This will return a confidence array for all possible classes for both golden output and corrupted output for easy comparison.

## Parameters

None.

## Return

A list of lists, containing the considered classes and the confidence level of detection for the respective class. The first list is for the golden output, and the second is for the corrupted output.
