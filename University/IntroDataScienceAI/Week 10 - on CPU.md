Loading data can run both on CPU and GPU, but to make it more efficiently, we want to move this process to the GPU

`cuda` : GPU of nvdia
Function `my_tensor.to('cuda')` since the my_sensor variable still in the CPU, so we have to return it
However, the `model = PyTorchMLP()`
`model = PyTorchMLP(num_features=784, num_classes=10)` **Still in CPU**
Only when u call `model.to('cuda')` *Now it is moved to GPU*
