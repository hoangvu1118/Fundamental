
- Vector, matrix, multi-array (tensor) computations
- Base computation for ML libraries: [scikit-learn](https://scikit-learn.org/stable/index.html)
- Tensor computations → pytorch, tensorflow

### Using list comprehension to create a dictionary to count frequency:
```python
s = "hello ho"
frequence = {char : s.count(char) for char in sorted(s) if char != ' '}
print(frequence) # {'e': 1, 'h': 2, 'l': 2, 'o': 2}
```

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
- AXIS 0 is vertical
- AXIS 1 is horizontal
- This is for 2D array
### EXPLANATION
```Python
import numpy as np
# Create the array
out = np.array([
    [[1, 2, 3, 4],   # Layer 1
     [5, 6, 7, 8],
     [9, 10, 11, 12]],

    [[10, 20, 30, 40],  # Layer 2
     [50, 60, 70, 80],
     [90, 100, 110, 120]]
])
print("Original shape:", out.shape)  # (2, 3, 4)

# Sum along axis 0
result = out.sum(axis=0)
print("Result shape:", result.shape)  # (3, 4)
print("Result:\n", result)

```
- `out[0]` (Layer 1) has shape **(3, 4)**.
- `out[1]` (Layer 2) has shape **(3, 4)**.
- When you sum along `axis=0`, the two layers get added element-wise:
```
[[ 11  22  33  44] 
 [ 55  66  77  88]  
 [ 99 110 121 132]] --> this is (3,4)
 ```
## Function NameNaN-safe Version  

| np.sum              | np.nansum                                                                                                                   |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| May have some error | It will place "nan" if there is any error but not stop the program --> it ignore that bugs and add the sum of other numbers |

## Slicing and Indexing

## using np.where
`feature[np.where(feature[:,2] != 0)]` : this one will check where the value at index will be different from zero 
then return the new array to assign for the new array

```python
import torch 
import numpy
a = np.array([1,2,3], [4,5,6], [5,6,7])
np.where(a!=3)
--> print # [0,0,1,1,1,2,2,2], [0,1,0,1,2,0,1,2]
--> the first array is x index and second array is y index
--> so u can see the value 3 at index (0,2) is missing

a[np.where(a!=3)] = 1
--> this one different ==> this will print the 2D array but other value != 3 will become 1 
--> [1,1,3,
	 1,1,1,
	 1,1,1]

np.where(a[:,2] != 6) ---> so it will filter out all the row and upto 2 columns(inclusion) --> and check if which one does not have 6
->> print out # [0,2] whhich mean row 0 and row 2 does not have 6

a[np.where(a[:,2] != 6) --> print out the matrix with first and last document 

np.where(a[1, :] != 6) # go to row 2 [4,5,6] --> iterate all col --> print out [0,1] which is 4 and 5
	# 2d index -> id index for column

a[:, np.where(a[1,:] != 6)[0]] # filter array
The condition means to extract: [0, 1] from (array([0, 1]),)
### `a[:, [0, 1]]`
This means: select all rows (`:`), but only columns `0` and `1`.
``` 

