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
					[2.,3.,4.]
				  [[5.,6.,7.],
					[8.,9.,10.]]]])
a.shape --> torch.Size([2,2,3])
```
Each number return 1 dimension -> 1 rank and its represent number of element in that rank

### 4D Tensor - Rank-4 tensor
multiple image stack up together
`b = torch.stack((a,a))`

Similar to numpy


# Perceptron model
![[Pasted image 20250416225330.png | 300]]
So the sum is calculated by summing up the two inputs (x1, x2) 
From there on, we consider the model parameter (bias)
--> the `>0` if yes -> update the output the perceptron

## Different view 
### Model Parameters
![[Pasted image 20250410091611.png | 400]]
Explanation
So the x1, x2 are inputs
We want to calculated for the **Weighted Sum**
First we need to calculate the input
By multiplying each input to its own *w*
Then we add these input up and with also the bias (B) 
--> This form a *WEIGHTED SUM* 
--> We then check if it is larger than 0 or not
**THE process is called FORWARD**

![[Pasted image 20250416225914.png]]
This graph is a combination of computing error and update model parameters
First we need to computing for errors
This is calculated by subtracting the predicted value *y hat (pink one)* by the true value (Y)
so Y is the value we want the model to predict
and *Y hat* is what it produce
We then calculate this error and update the bias and weight parameter

# Model Training - Minimize the Loss
![[Pasted image 20250416231833.png | 450]]
Given value x1 and y
--> update w1 and b to minimize the loss

Goal : minimize to 1.0
By updating b and w1
Calculating net input -> to calculate u and see how it affecting the error
--> calculate partial derivative to the slope 
We use chain rule 
breakdown to individual steps from the Loss (y) ![[Pasted image 20250416232751.png | 400]]

### Derivative vs Gradient
**Partial Derivative** : This will help us calculating the derivative of a function that have more than 1 variable
![[Pasted image 20250416233148.png | 400]]
**Gradient** : This will store the result of each of the partial derivative in to a vector form (an array)
![[Pasted image 20250416233333.png | 450]]

### Automatic Differentiation in PyTorch
requires_grad : the gradient of the loss with respect to these parameters
![[Pasted image 20250416234550.png | 450]]
**Inputs and weigh + bias**

![[Pasted image 20250416234623.png | 450]]
**Compute the weighted sum**

![[Pasted image 20250416234715.png | 450]]
**Sigmoid activation function**

![[Pasted image 20250416234751.png]]
**Calculate the loss**
--> feed in the net input instead of the activation function
So the program will calculate the sigmoid activation function internally

![[Pasted image 20250416234941.png | 350]]

Compute the gradient automatically
retain_graph: retain the graph in still in memory
--> we want to calculate the partial derivative with respect to w1 and b

**Instead of calculating these manually**
We use L.backward()
We will calculate the loss then call l.backward()
![[Pasted image 20250416235013.png | 350]]

## Minimize Loss Using Gradient Descent
Recap : epoch is an iteration of over the training set
->> we need multiple epoch to minimize the loss
 
