## Why data loader ?
+ Loading and processing input data is time consuming
	+ Load all data before training? not efficient 
		+ Initial time wasting
		+ Memory consumption
+ Solution: Load in training loop but do it parallel -> do not block the computation
Divide into **mini-batch**
Random shuffle (important for mini-batch and stochastic update)

Computer components : GPU and CPU
CPU : to load and prepare the data 
GPU : do the computation
both of these happens parallelly so no one is blocked

![[Pasted image 20250423223817.png | 350]]
Workflow of data training 
Problem: The data might get paused for few moments due to large size of data set 
--> Solution: we want it to have different processes
-> Then we will have the data be ready for the next iteration(next minibatch)

![[Pasted image 20250423224042.png| 400]]

Process workflow
First read image -> put 'em' in the memory then transform it into learnable data by using pytorch 
-> it'll become a vector ...
So if the minibatch size is *32* then the CPU has to load and process 32 images and then they can do the computational part


The train_loader is a method of the class ... 
So it will help us preparing the next dataset while we iterating the current dataset 
![[Pasted image 20250423224405.png | 400]]
So number of workers : number of background process that will work to prepare the dataset for next iteration
drop_last : to chop the minibatch if the dataset not evenly divisible by the batchsize

![[Pasted image 20250424093806.png | 500]]
![[Pasted image 20250424095504.png | 400]]
Dataset is used first to get the data
-> then we train this data by calling an instance of DataLoader()

The dataset class define how the data is loaded and process
So first shuffle the index, and the class dataset is used to feed the machine with these transformed dataset
From the data loader, we can use _getitem_ (index) to retrieve the data 

