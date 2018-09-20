---
layout: post
title: Jupyter notebook with the virtual environment
---

## Steps to make jupyter notebook run with the virual env.

### 1. Create the virtual environment

> conda create -n env_name python=3.6

### 2. Actiavte the venv

> conda activate env_name

### 3. Install the kernel that uses the virtual env

> python -m ipykernel install  --name env_name --display-name user_friendly_env_name

### 4. Start the jupyter notebook

> jupyter notebook

### 5. Choose the kernel from the UI

#### Test

```python
import sys
print(sys.executable)
```

### Deactivate the venv

> conda deactivate

## FAQ

1. I have installed a new package in the virtual environment. But, it is showing `module not found` error in the notebook. What should I do?

- In most of the cases, just restarting the kernel in the jupyter notebook shall fix the issue. If the problem still persist, then try unistalling the package that is not being loaded and check its installed location. If the location is not inside the virtual env. try unistalling completely and install fresh.
