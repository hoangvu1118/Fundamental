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


