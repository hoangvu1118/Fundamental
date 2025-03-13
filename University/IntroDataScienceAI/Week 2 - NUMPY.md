
- Vector, matrix, multi-array (tensor) computations
- Base computation for ML libraries: [scikit-learn](https://scikit-learn.org/stable/index.html)
- Tensor computations → pytorch, tensorflow

### Why multidimensional Array:
Images : 2D array --> Compute parallelly --> on the GPU
Sound, time series data: 1D array
--> Sequential data: Time Series Data

Text : 1D array
→ All kind of data can be converted to numerical array

## Numpy syntax
Multi-dimensional array : ndarray
```python
c = []
for i in range(len(a)):
    c.append(a[i]*b[i]) # C = a * b
```
**LIST vs Numpy**
List can store dynamic types
List = `[True, "2", 3.0, 4]`

NumPy arrays: all contain the same type
`np.array([1, 2, 3, 4], dtype='float32')`


Shape: shape
Number of dimensions: ndim
Data size: size
Type: The elements are all of the same type, referred to as the array dtype.

```python
out = np.random.rand(2,3) # create a random ndimension-array
out.shape # print the shape (2,3)
out.ndim # the dimension --> 2 (row)
out.size # total number of elements 6
out.dtype # dtype(['float64'])
# to type casting data type
out.astype(int)
	out.dtype #dtype('int64')
```
**Dimensions are called axes.**
```python
a = [[0., 0., 0.],  #a[2][3]
        [1., 1., 1.]]
Your array has 2 axes.
**
The first axis has a length of 2 and 
the second axis has a length of 3.
**
```