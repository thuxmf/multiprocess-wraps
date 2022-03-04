# Multiprocess V0.8

## What is it?

It is a package for easily using multiprocess.

## Usage

One can use this package as the **function** of you function, which is much easier than to implement the multiprocess pool or process. For example:

```python
def original_function(x, y=0, z=0):
    return x + y + z

import multiprocess
multiprocess_function = multiprocess(original_function)
```

To call the function, simply using

```python
# original version
# return value: 1
origigal_function(1)

# multiprocessing version
# return value: [1, 2, 3]
multiprocess_function([1, 2, 3])
```

**However, always remember to change the name since we use the `__call__` which will leads to the `_pickle.PicklingError`.**

One can also specify the number of workers or whether to involvo CUDA by

```python
# use `min(8, cpu_count())` workers, 
func_multi = multiprocess(func, 8)

# print some information for understanding or debugging
func_multi = multiprocess(func, verbose=True)

# involve CUDA
func_multi = multiprocess(func, cuda=True)
```

Notice that the input parameters are iterators with the same length, so when using `torch.Tensor` you may need to adjust the output or the input, e.g.,

```python
def func(x, y=0, z=0):
    return x + y + z

func_multi = multiprocess(func)
print(func_multi(torch.ones(2, 3)))
# return value: [tensor([1., 1., 1.]), tensor([1., 1., 1.])]
# i.e,. [torch.ones(3), torch.ones(3)]
```
## TODOs:

- [ ] Setting `gpu_ids`for multiprocessing with CUDA involved.