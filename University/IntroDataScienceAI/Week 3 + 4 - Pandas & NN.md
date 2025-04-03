# Week 4 - Intro to Neural Networks
#pytorch
### Machine learning : model with weights (parameter)

###### Classic Program : input -> *program* -> results
-> only handle 1 single task (downside of classic program)

###### Solution -> Model with weights
- ML models
- Neural networks
-> Universal program
So if we change the *weights* --> it can make the program run differently
--> no need to write new program -> just need to adjust the weight
**input + weight -> model -> results**

### Learn by update weight
![[Pasted image 20250403091344.png | 450]]
--> get better performance by updating the weights

### Machine learning tasks
![[Pasted image 20250403091558.png]]
*OUPUT*
Classification : the categories
Regression: the values
Clustering : grouping the elements into sets

#### How to learn from data ?
*Supervised learning* (data with labels)
- Input/ features
- Output/ targets (labels)
*Unsupervised learning* (data w/o labels)

### Measure performance
+ Training and test data
+ Underfit/ Overfit
## Pattern Classification
- Which category of an input?
	- Example: Character recognition for input images
![[Pasted image 20250403103203.png | 400]]

### Supervised learning
+ Learn by a training dataset
	+  pair<input, target>
+ Testing on unseen dataset --> generalization ability
![[Pasted image 20250403103748.png | 300]]

Relearn gradient descend 
