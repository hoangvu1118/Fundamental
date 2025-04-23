## Require_grad
Think of `requires_grad=True` as telling PyTorch: "Hey, I want you to keep track of all the operations you perform on this tensor. I'm going to need to calculate gradients with respect to it later."

When you set `requires_grad=True` for a tensor, you're essentially *building a computational graph.* Every operation you perform involving this tensor is recorded in this graph.

If `w_1` and `b` don't have `requires_grad=True`, When you eventually calculate the loss and call `.backward()` on it, PyTorch *will traverse* this computational graph _backwards_ to compute the gradients of the loss with respect to all tensors that have `requires_grad=True`.

If `w_1` and `b` don't have `requires_grad=True`, t*hey won't be part of the computational graph* that PyTorch uses for gradient calculation. Consequently, when you call `.backward()`, `w_1.grad` and `b.grad` will be `None`
## Gradient descent vs Stochastic gradient descent
1. for former -> update one time after going through all the sample
2. for latter -> update each time it go through 1 sample
3. Practical type : Minibatch : each minibatch(m-sample) ->update once
Data in minibatch should be shuffle so that it can be trained to make it more generalize
![[Pasted image 20250417093536.png | 200]]![[Pasted image 20250417093526.png | 200]]![[Pasted image 20250417093510.png | 250]]


## Hidden Layer
### Linear Layer
![[Pasted image 20250417110644.png | 300]]![[Pasted image 20250417111126.png | 300]]

Code demonstration for this AI model -> that has 2 hidden layers
linear1 is the variable in train to create 2 inputs to make 4 output for the second layer
the second layer then train these 4 input to the last 2 output
final layer convert these 2 layers into the final output
ReLu is an activation function that use to generate the overall_loss

![[Pasted image 20250417111339.png | 300]]
So each input will give an ouput (imagine it is a pixel of an image)
So here teachers inputted 3 inputs so it results in 3 outputs


## Pytorch API

![[Pasted image 20250423215349.png | 250]]

So the class will be inherited from the torch.nn.module
That will give us all of the properties needed for the calculation
+ Self.init: to create parameters
+ Forward function : pass in data point x and define the model do the prediction

The use of Stochastic Gradient Descent
![[Pasted image 20250423215727.png | 350]]

Create an instance model 
and an optimizer that use Stochastic Gradient Descent 
+ That is to update the variable (the input)

Workflow:
+ Iterate through each epoch 
	+ And then feed the input x and the result y from the train_dataloarder ( this will give us the minibatches for us)
+ Then we calculating the model OUTPUT (weighted sum) and then calculating the loss
+ After calculating the loss 
	+ Call zero_grad on optimizer - reset the gradient
	+ backward calculating the gradient - chain rule
	+ and optimizer.step() update the model parameter 

![[Pasted image 20250423221258.png | 450]]
Neural network layer : Layer to compute the weighted sum
![[Pasted image 20250423221411.png | 350]]
Compute the weighted sum by calling *linear(x)*

>[!Tip] With torch.no_grad() :
>This will disabling the pytorch function to save the computation in the graph -> so we dont want it to be in the graph when we call the loss.backward() later on. 
>

![[Pasted image 20250423223817.png | 350]]
Workflow of data training 
Problem: The data might get paused for few moments due to large size of data set 
--> Solution: we want it to have different processes
-> Then we will have the data be ready for the next iteration(next minibatch)

![[Pasted image 20250423224042.png| 400]]
The train_loader is a method of the class ... 
So it will help us preparing the next dataset while we iterating the current dataset 
![[Pasted image 20250423224405.png | 400]]
So number of workers : number of background process that will work to prepare the dataset for next iteration
drop_last : to chop the minibatch if the dataset not evenly divisible by the batchsize
