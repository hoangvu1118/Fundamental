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
**Computational graph**
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
This *computation graph* is a combination of computing error and update model parameters
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

![[Pasted image 20250517231229.png | 250]] ![[Pasted image 20250517231256.png | 300]]
Slope in 2 dimensions , the gradient of the partial derivative is a vector of 2 derivative

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
so logist is for the lost that is not normalized

![[Pasted image 20250416234941.png | 350]]

Compute the gradient automatically
retain_graph: retain the graph in still in memory
--> we want to calculate the partial derivative with respect to w1 and b

**Instead of calculating these manually**
We use L.backward()
We will calculate the loss then call l.backward()
![[Pasted image 20250416235013.png | 350]]

Code
```Python
import torch
w1= torch.tensor(0.23, requires_grad = True)
b = torch.tensor(0.1, requires_grad = True)

# inputs and target --> no need to check --> no need requires_grad
x1 = torch.tensor(1.23)
y = torch.tensor(1.)

u = x1 * w1
z = u + b
print(z)

a = torch.sigmoid(z)
print(a)

import torch.nn.functional as F
l = F.binary_cross_entropy_with_logits(z, y) # reflect how wrong the program is
w1.grad, b.grad
```
## Minimize Loss Using Gradient Descent
Recap : epoch is an iteration of over the training set
->> we need multiple epoch to minimize the loss
![[Pasted image 20250417101441.png | 370]]

So the program iterate through multiple epoch to minimize the loss
At each epoch we set the over_loss to 0 to calculate the loss
from that point we iterate through examples(samples) 
	at each example -> we will calculate the activate function output
		Then use this to update overall_loss at each example 
		Eventually we normalize the over_loss by dividing it by n 
Finally, we compute the gradient of this loss and the bias
--> use these gradient to update the parameters

For perceptron -> we use error to update the parameter
For gradient descent -> we use the gradient of over_loss to update 
$\alpha$ is a learning rate -> allow the program to learn at a small rate to avoid volatile

Stochastic Gradient Descent is *main component* of back propagation
*Back propagation* is most popular learning algorithm for Deep Neural Networks
```python
for each_training in epoch: #Epoch is 1 iteration over the training set -> we need multiple epoch
    overall_loss_L = 0
    for each_train_example: # iterate through training example
        output = Φ(z)   # calculate the activation function
        overall_loss_L = overall_loss_L + l(output, label) # calculate the loss value
        # We summing the overall_loss
    overall_loss_L = overall_loss_L / n # bring to normal scall for later
    #Normalize the loss 
    #This will COMPUTE the loss over the training example

    #Then update parameters once per epoch
```
## Using Stochastic GD
Update more frequently than batch/gradient descent
Code is slightly similar to the *batch*

Better solution : Most ideal -> Minibatch Gradient Descent
Hybrid = Batch + Stochastic
The size of minibatch(m) are multiple of 2 
So they make it fit to the GPU architecture for computation
### Minibatch
```python
For each training epoch:
    for each minibatch:
        overall_loss_L = 0
        for each training example in minibatch:
            output = Φ(z)
            overall_loss_L = overall_loss_L +  l(output, label)
        overall_loss_L = overall_loss_L / n;
        #then update parameters

# Explanation
This is very somewhat similar to the gradient descent approach
However with frequent updates, parameters will get adjusted after every the minibatch
```
Much better GPU utilization

w1.grad -> the slop of w1 -> so that it decrease to 1


>[!warning]
>When calling loss.backward() we have to pay attention to before
Normally, loss is calculated first -> and this should be a scalar instead of any vector so that we can start calculate the backward to start optimize the loss
 So if the loss that is not in a scalar form -> it might be vector or something ->
 We have to use loss.mean() or loss.sum() before calling loss.backward() to avoid error
 

The x.grad called after the function.backward() -> mean that the x will store a value of 
the change of the function with respect to x
say x = 2 ->> then the function x^2 + 3x + 8 would be 7(after calculating the derivative of f(x) --> 2x + 3) then x.grad = 7 
Which is how the function react on the tiny change on the input `x`

**`loss.backward()`**: This is the **backward pass**. PyTorch's autograd engine calculates the gradients of the `loss` with respect to all the model's parameters (those with `requires_grad=True`). These gradients are stored in the `.grad` attribute of each parameter.

**torch.optim.SGD(model.parameters(), lr=0.01)** : an Optimizer 
--> adjust the model's parameters *(weights and biases)* in a way that minimizes the loss function.

**Objective**
1. **Problem Definition and Goal Setting:** Clearly understand what you want to achieve.
2. **Data Collection and Preparation:** Gather, clean, and transform your data.
3. **Model Selection/Definition:** Choose or design your model architecture.
4. **Defining Loss Function and Optimizer:** Specify how to measure error and update the model.
5. **Training the Model:** The iterative process of learning from data.
6. **Evaluation:** Assess how well your model performs.
7. **Hyperparameter Tuning and Iteration:** Optimize your model.
8. **Making Predictions (Inference):** Use your trained model on new data.
9. **Deployment and Monitoring (Brief Overview):** Put your model into production.

>[!Important] Machine Learning Workflow

**Step 2: Data Collection and Preparation**
Data is the fuel for machine learning.
- **Data Acquisition:** Collect relevant data. This could be from databases, APIs, files (CSV, JSON, images), web scraping, etc.
- **Data Exploration and Visualization:** Understand your data's structure, distributions, and potential issues. Libraries like Pandas, Matplotlib, and Seaborn are useful here.
- **Data Cleaning:**
    - Handle missing values (imputation, removal).
    - Handle outliers (detection, treatment).
    - Correct errors or inconsistencies.
- **Feature Engineering (Optional but often crucial):**
    - Create new informative features from existing ones (e.g., calculating a sum or average of grades).
    - Transform features to make them more suitable for the model (e.g., log transformation).
- **Data Splitting:** Divide your dataset into three parts:
    - **Training Set:** Used to train the model. (e.g., 70-80% of data)
    - **Validation Set (or Development Set):** Used to tune hyperparameters and make decisions about the model architecture during training. It helps prevent overfitting to the training set. (e.g., 10-15%)
    - **Test Set:** Used for a final, unbiased evaluation of the trained model's performance on unseen data. (e.g., 10-15%)
    - _Important:_ The test set should only be used _once_ after all training and tuning are complete.
- **Data Transformation/Preprocessing:**
    - **Scaling/Normalization:** For numerical features, scale them to a common range (e.g., 0-1 or mean 0, std 1). This helps optimizers converge faster and prevents features with larger values from dominating. (e.g., `StandardScaler`, `MinMaxScaler` from `sklearn.preprocessing`).
    - **Encoding Categorical Features:** Convert non-numerical features into a numerical format (e.g., One-Hot Encoding, Label Encoding).
- **Creating PyTorch Datasets and DataLoaders:**
    - `torch.utils.data.Dataset`: An abstract class for representing a dataset. You'll often create a custom class inheriting from this.
    - `torch.utils.data.DataLoader`: Wraps a `Dataset` and provides an iterable over the dataset, handling batching, shuffling, and parallel data loading.

```python
import torch
from torch.utils.data import Dataset, DataLoader, random_split
# --- Example: Dummy Data ---
 train_x_full = torch.randint(1, 10, (100, 5), dtype=torch.float32) # 100 students, 5 grades
 train_y_full = (train_x_full.sum(1) > 25).float().unsqueeze(1) # Target: 1 if sum > 25, else 0
# --- Custom Dataset ---
class GradesDataset(Dataset):
    def __init__(self, features, labels):
        self.features = features
        self.labels = labels

    def __len__(self):
        return len(self.features)

    def __getitem__(self, idx):
        return self.features[idx], self.labels[idx]

# --- Data Splitting ---
 dataset_full = GradesDataset(train_x_full, train_y_full)
 train_size = int(0.7 * len(dataset_full))
 val_size = int(0.15 * len(dataset_full))
 test_size = len(dataset_full) - train_size - val_size
 train_dataset, val_dataset, test_dataset = random_split(dataset_full, [train_size, val_size, test_size])

# --- DataLoaders ---
 batch_size = 16 # Number of samples processed before the model is updated
 train_loader = DataLoader(dataset=train_dataset, batch_size=batch_size, shuffle=True)
 val_loader = DataLoader(dataset=val_dataset, batch_size=batch_size, shuffle=False)
 test_loader = DataLoader(dataset=test_dataset, batch_size=batch_size, shuffle=False)

print(f"Number of training batches: {len(train_loader)}")
print(f"Number of validation batches: {len(val_loader)}")
print(f"Number of test batches: {len(test_loader)}")
```

**Step 3: Model Selection/Definition**
Choose or build the model architecture.
- **Choosing a Model Type:**
    - Simple problems: Linear Regression, Logistic Regression.
    - Complex patterns, image/text data: Neural Networks (Feed-forward, CNNs, RNNs, Transformers).
- **Defining a Neural Network in PyTorch (using `nn.Module`):**
    - Create a class that inherits from `torch.nn.Module`.
    - Define layers in the `__init__` constructor (e.g., `nn.Linear`, `nn.Conv2d`, `nn.ReLU`, `nn.Sigmoid`).
    - Implement the `forward` method to define how data flows through the layers.

```Python
import torch.nn as nn
class SimpleNN(nn.Module):
    def __init__(self, input_size, hidden_size, num_classes):
        super(SimpleNN, self).__init__()
        # Define layers
        self.fc1 = nn.Linear(input_size, hidden_size) # First fully connected layer
        self.relu = nn.ReLU()                         # Activation function
        self.fc2 = nn.Linear(hidden_size, num_classes) # Output layer
        # For binary classification with BCELoss, the output layer might have 1 unit,
        # followed by a Sigmoid in the forward pass or as part of the loss function.
        # If num_classes=2 and using CrossEntropyLoss, often no explicit sigmoid/softmax here.
    def forward(self, x):
        # Define the forward pass
        out = self.fc1(x)
        out = self.relu(out)
        out = self.fc2(out)
        # If using BCELoss for binary classification, and fc2 has 1 output unit:
        # out = torch.sigmoid(out)
        return out

# Example instantiation:
input_dim = 5  # Number of features from our grades data
hidden_dim = 32 # You choose this
output_dim = 1   # For binary classification with BCELoss and a final sigmoid
model = SimpleNN(input_dim, hidden_dim, output_dim)
print(model)
```

- **Weight Initialization:** PyTorch layers have default weight initializations (e.g., Kaiming He initialization for `nn.Linear`). You can customize this, but defaults are often a good start.

**Step 4: Defining Loss Function and Optimizer**
- **Loss Function (`criterion`):** Measures how different the model's output is from the true target.
    - `nn.BCELoss()`: Binary Cross Entropy Loss (for binary classification, expects model output to be probabilities from a Sigmoid).
    - `nn.BCEWithLogitsLoss()`: Combines Sigmoid and BCELoss (more numerically stable, expects raw logits from the model).
    - `nn.CrossEntropyLoss()`: For multi-class classification (combines LogSoftmax and NLLLoss, expects raw logits).
    - `nn.MSELoss()`: Mean Squared Error (for regression).

- **Optimizer:** Implements an algorithm to update model weights based on the gradients computed from the loss.
    - `torch.optim.SGD(model.parameters(), lr=learning_rate)`: Stochastic Gradient Descent.
    - `torch.optim.Adam(model.parameters(), lr=learning_rate)`: A popular adaptive learning rate optimizer.
    - `torch.optim.RMSprop`, `torch.optim.Adagrad`, etc.

``` Python
 --- Assuming 'model' is an instance of your nn.Module subclass ---
 --- And the task is binary classification with a final sigmoid in the model ---

# model = SimpleNN(input_dim, hidden_dim, output_dim) # As defined before

 learning_rate = 0.01
 criterion = nn.BCELoss() # If model's forward pass includes the final sigmoid
 # If model outputs raw logits (no final sigmoid):
  criterion = nn.BCEWithLogitsLoss()
 optimizer = torch.optim.Adam(model.parameters(), lr=learning_rate)
```

**Step 5: Training the Model (The Training Loop)**
This is where the model learns.
- **Iterate through Epochs:** An epoch is one complete pass through the entire training dataset.
- **Iterate through Batches:** Process data in mini-batches (from the `DataLoader`).
- **For each batch:**
    1. **Move data to device (GPU/CPU):** `inputs, labels = inputs.to(device), labels.to(device)`
    2. **Forward Pass:** Get predictions from the model: `outputs = model(inputs)`
    3. **Calculate Loss:** Compute the loss: `loss = criterion(outputs, labels)`
    4. **Zero Gradients:** Clear old gradients: `optimizer.zero_grad()`
    5. **Backward Pass (Backpropagation):** Compute gradients of the loss w.r.t. model parameters: `loss.backward()`
    6. **Optimizer Step:** Update model parameters: `optimizer.step()

- **Logging:** Track loss and other metrics (e.g., accuracy on the training or validation set) to monitor progress.
``` Python
# --- Example Training Loop ---
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
model.to(device) # Move model to the chosen device

num_epochs = 10 # You choose this

for epoch in range(num_epochs):
     model.train() # Set model to training mode (important for layers like Dropout, BatchNorm)
     running_loss = 0.0
     correct_train_predictions = 0
     total_train_samples = 0

     for i, (inputs, labels) in enumerate(train_loader): # Iterate over batches
         inputs = inputs.to(device)
         labels = labels.to(device)

         # Forward pass
         outputs = model(inputs) # If model includes sigmoid, outputs are probabilities
         loss = criterion(outputs, labels)

         # Backward and optimize
         optimizer.zero_grad()
         loss.backward()
         optimizer.step()

         running_loss += loss.item() * inputs.size(0) # Accumulate loss

         # For accuracy (example for binary classification)
         predicted = (outputs >= 0.5).float() # Threshold probabilities
         correct_train_predictions += (predicted == labels).sum().item()
         total_train_samples += labels.size(0)

     epoch_loss = running_loss / total_train_samples
     epoch_acc = correct_train_predictions / total_train_samples
     print(f"Epoch [{epoch+1}/{num_epochs}], Train Loss: {epoch_loss:.4f}, Train Acc: {epoch_acc:.4f}")

    # --- Validation (Optional, but highly recommended after each epoch) ---
     model.eval() # Set model to evaluation mode
     with torch.no_grad(): # Disable gradient computation
         val_loss = 0.0
         correct_val_predictions = 0
         total_val_samples = 0
         for inputs_val, labels_val in val_loader:
             inputs_val = inputs_val.to(device)
             labels_val = labels_val.to(device)
             outputs_val = model(inputs_val)
             loss_val_batch = criterion(outputs_val, labels_val)
             val_loss += loss_val_batch.item() * inputs_val.size(0)

             predicted_val = (outputs_val >= 0.5).float()
             correct_val_predictions += (predicted_val == labels_val).sum().item()
             total_val_samples += labels_val.size(0)

         epoch_val_loss = val_loss / total_val_samples
         epoch_val_acc = correct_val_predictions / total_val_samples
         print(f"Epoch [{epoch+1}/{num_epochs}], Val Loss: {epoch_val_loss:.4f}, Val Acc: {epoch_val_acc:.4f}")
```

**Step 6: Evaluation**

Assess your model's performance on unseen data (validation set during training, test set after final training).
- **Set Model to Evaluation Mode:** `model.eval()`. This is crucial for layers like Dropout (which is turned off) and Batch Normalization (which uses running statistics).
- **Disable Gradient Calculation:** Use `with torch.no_grad():` to speed up computation and reduce memory usage, as gradients are not needed for evaluation.
- **Iterate through the evaluation data (validation or test loader).**
- **Perform a forward pass to get predictions.**
- **Calculate your chosen evaluation metrics** (accuracy, precision, recall, F1-score, MSE, etc.).

``` Python
# --- Example Evaluation on Test Set (after all training and tuning) ---
 model.eval() # Ensure model is in evaluation mode
 test_predictions_list = []
 test_labels_list = []
 total_test_loss = 0.0
 correct_test_predictions = 0
 total_test_samples = 0

 with torch.no_grad():
     for inputs_test, labels_test in test_loader:
         inputs_test = inputs_test.to(device)
         labels_test = labels_test.to(device)

         outputs_test = model(inputs_test)
         loss_test_batch = criterion(outputs_test, labels_test) # Can still compute loss if needed
         total_test_loss += loss_test_batch.item() * inputs_test.size(0)

         predicted_test_probs = outputs_test
         predicted_test_classes = (predicted_test_probs >= 0.5).float()

         test_predictions_list.extend(predicted_test_classes.cpu().numpy())
         test_labels_list.extend(labels_test.cpu().numpy())

         correct_test_predictions += (predicted_test_classes == labels_test).sum().item()
         total_test_samples += labels_test.size(0)

 final_test_loss = total_test_loss / total_test_samples
 final_test_accuracy = correct_test_predictions / total_test_samples
 print(f"Final Test Loss: {final_test_loss:.4f}")
 print(f"Final Test Accuracy: {final_test_accuracy:.4f}")
# # You can use sklearn.metrics for more detailed evaluation
# from sklearn.metrics import classification_report
# # print(classification_report(test_labels_list, test_predictions_list))
```

**Step 7: Hyperparameter Tuning and Iteration**
Improve your model by adjusting settings that are not learned during training.
- **Hyperparameters to Tune:**
    - Learning rate
    - Batch size
    - Number of epochs
    - Number of layers and units per layer in a neural network
    - Optimizer choice
    - Activation functions
    - Regularization strength (e.g., weight decay for L2 regularization)

- **Techniques:**    
    - **Manual Search:** Try different values based on intuition and observation.
    - **Grid Search:** Define a grid of hyperparameter values and try all combinations.
    - **Random Search:** Sample hyperparameter values randomly from specified distributions.
    - **Bayesian Optimization / Automated ML (AutoML) tools.**
    
- **Use the Validation Set:** All hyperparameter tuning should be guided by performance on the validation set, _not_ the test set.
- **Saving and Loading Models:**
    - Save your best model's state (weights and biases) so you can reuse it later without retraining.

``` Python
# --- Saving the model ---
 model_save_path = "my_best_model.pth"
 torch.save(model.state_dict(), model_save_path)
 print(f"Model saved to {model_save_path}")

# --- Loading the model ---
 loaded_model = SimpleNN(input_dim, hidden_dim, output_dim) # Create an instance of the same model class
 loaded_model.load_state_dict(torch.load(model_save_path))
 loaded_model.to(device) # Move to device
 loaded_model.eval() # Set to evaluation mode
 print("Model loaded successfully.")
```

- **Iteration:** Machine learning is an iterative process. You might go back to data preparation, feature engineering, or model architecture design based on your evaluation results.

**Step 8: Making Predictions on New Data (Inference)**
Once you have a trained and satisfactory model, you can use it to make predictions on new, unseen data for which you don't have labels.
- The process is similar to evaluation:
    - Load your trained model.
    - Set it to `model.eval()`.
    - Use `with torch.no_grad():`.
    - Preprocess the new input data in the _exact same way_ you preprocessed your training data.
    - Pass the data through the model to get predictions.
    - Post-process the predictions if necessary (e.g., convert probabilities to class labels).