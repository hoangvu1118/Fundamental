## Tensors
data container that store multidimensional array

### Scalar - rank-0 tensor
Python : a = 1. 
pytorch:  a = torch.tensor(1.) 
			print(a.shape) --> torch.Size([])
--> rank 0 so no size

### Vector - rank-1 tensor / 1 dimension
Python: a = `[1., 2., 3.]`
Pytorch: a = `torch.tensor([1., 2., 3.])`
			->torch.Size(`[3]`)

### Matrix - rank-2 tensor
Pytorch: a = torch.tensor(`[1., 2., 3.],
					`[2., 3., 4.])
Real World -> row|columns -> pixels

### 3D Tensor - rank-3 tensor
![[Pasted image 20250416224639.png | 300]]
So each layer(read/ green/ blue) is a matrix
Pytorch
```python
a = torch.tensor([[[1.,2.,3.],
					[2.,]]])
```