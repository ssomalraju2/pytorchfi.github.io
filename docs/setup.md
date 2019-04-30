---
layout: default
title: Setup
nav_order: 2
---

# Setting Up PyTorchFI

## Requirements for PyTorchFI

- Python 3
- PyTorch 1.0

## Installing PyTorchFI

### Via Pip

Install using `pip install pytorchfi` Then in your project source files:

```python
import pytorchfi
```

### From Source

Download the source code [here](https://github.com/pytorchfi/pytorchfi), and add the directory into the root of your project.

At the top of any file you wish to use PyTorchFI in, add

```python
from src import PyTorchFI_Util as pytorchfi
```

You will then be able to call the available functions from `pytorchfi`.
