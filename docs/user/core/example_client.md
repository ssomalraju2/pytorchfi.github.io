---
layout: default
title: Example Core Client
parent: PyTorchFI.Core
grand_parent: Using PyTorchFI
nav_order: 4
---

# PyTorchFI.Core Example Client

The following is an example client on how to use the full functionality of PyTorchFI.Core.

```python
from src import PyTorchFI_Source_Core as pytorchfi

if __name__ == "__main__":
    model = load_pretrained(AlexNet(), PRETRAINED_PATH, False)
    input = Variable(CIFAR10_dataset(BATCH_SIZE)[0])
    softmax = nn.Softmax(dim=1)

    "Golden Output"
    golden_output = model(input)
    golden_output_softmax = softmax(golden_output)
    golden = list(torch.argmax(golden_output_softmax, dim=1))

    pytorchfi.init(model, 32, 32, 1)

    "Single Specified Fault Injection"
    model = pytorchfi.declare_fi(
        conv_num=2, batch=0, c=2, h=1, w=1, value=10000000000000
    )

    single_corrupted_output = model(input)
    single_corrupted_output_softmax = softmax(single_corrupted_output)
    single_corrupted = list(torch.argmax(single_corrupted_output_softmax, dim=1))

    "List Specified Fault Injection"
    model = pytorchfi.declare_fi(
        conv_num=[1, 2],
        batch=[0, 0],
        c=[1, 2],
        h=[1, 1],
        w=[1, 1],
        value=[1392323, 10000000],
    )

    list_corrupted_output = model(input)
    list_corrupted_output_softmax = softmax(list_corrupted_output)
    list_corrupted = list(torch.argmax(list_corrupted_output_softmax, dim=1))

    "Randomized Fault Injection"
    model = pytorchfi.declare_fi()
    random_corrupted_output = model(input)
    random_corrupted_output_softmax = softmax(random_corrupted_output)
    random_corrupted = list(torch.argmax(random_corrupted_output_softmax, dim=1))

    "Custom Fault Injection"
    model = pytorchfi.declare_fi(function=set_zero)
    custom_corrupted_output = model(input)
    custom_corrupted_output_softmax = softmax(custom_corrupted_output)
    custom_corrupted = list(torch.argmax(custom_corrupted_output_softmax, dim=1))

    print("Expected vs Specified vs List Specified vs Random vs Custom")
    for index, predicted_val in enumerate(random_corrupted):
        print(
            "%s vs %s vs %s vs %s vs %s"
            % (
                CIFAR10_CLASSES[predicted_val],
                CIFAR10_CLASSES[single_corrupted[index]],
                CIFAR10_CLASSES[list_corrupted[index]],
                CIFAR10_CLASSES[random_corrupted[index]],
                CIFAR10_CLASSES[custom_corrupted[index]],
            )
        )
```

## Predefined Variables

1. `model`: model with pretrained weights loaded.

2. `input`: the dataset to be run with the model.

3. `softmax`: a function to determine the softmax of a tensor. Normally defined with `nn.Softmax(dim=1)`.

## Golden Output

Will run the model with the dataset before any injections are given, to determine the golden output to be compared to.

## Initializing PyTorchFI.Core

`pytorchfi.init(model, 32, 32, 1)` initializes the model with an image size of `32x32`.

## Single Specified Fault Injector

```python
model = pytorchfi.declare_fi(
        conv_num=2, batch=0, c=2, w=1, h=1, value=10000000000000
    )
```

This will return a model from PyTorchFI.Core that has injected the given fault injector at the specified location and value.

## List Specified Fault Injector

```python
model = pytorchfi.declare_fi(
    conv_num=[1, 2],
    batch=[0, 0],
    c=[1, 2],
    h=[1, 1],
    w=[1, 1],
    value=[1392323, 10000000],
)
```

## Randomized Fault Injector

`model = pytorchfi.declare_fi()` will declare a randomized fault injector in the model, which is because no parameters are given.

## Custom Injection

Given the function

```python
def set_zero(self, input, output):
    output = torch.IntTensor(output.size()).zero_()
```

then

```python
model = pytorchfi.declare_fi(function=set_zero)
```

will set all output tensors to zero.

## Comparing Output

The golden output, specified corrupted output, and randomized corrupted output are all compared with the following code:

```python
print("Expected vs Specified vs List Specified vs Random vs Custom")
for index, predicted_val in enumerate(random_corrupted):
    print(
        "%s vs %s vs %s vs %s vs %s"
        % (
            CIFAR10_CLASSES[predicted_val],
            CIFAR10_CLASSES[single_corrupted[index]],
            CIFAR10_CLASSES[list_corrupted[index]],
            CIFAR10_CLASSES[random_corrupted[index]],
            CIFAR10_CLASSES[custom_corrupted[index]],
        )
    )
```
