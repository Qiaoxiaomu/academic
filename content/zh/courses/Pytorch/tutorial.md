---
date: "2021-03-07"
title: 01 PyTorch Starter 
type: book
weight: 1
math: true
---

# Tesnsor -- Device
Default: tensors and modules will be computed with CPU

```python
import torch
device = 'cuda' if torch.cuda.is_available() else 'cpu'
print('Using {} device'.format(device))
```

    Using cpu device
    

# Dataset & Dataloader


```python
from torch.utils.data import Dataset, DataLoader
class MyDataset(Dataset):
   # Read data & preprocess
   def __init__(self, file):
       self.data = ...
    
   # Returns one sample at a time
   def __getitem__(self, index):
       return self.data[index]
    
   # Returns the size of the dataset
   def __len__(self):
       return len(self.data)

```


```python
dataset = MyDataset(file)
dataloader = DataLoader(dataset, batch_size, shuffle=True)
```
Training: shuffle=True
Testing:  shuffle=False


# Optimization

## How to Calculate Gradient


```python
x = torch.tensor([[1., 0.], [-1., 1.]], requires_grad=True)
print(x)
z = x.pow(2).sum()
z.backward()
x.grad
```

    tensor([[ 1.,  0.],
            [-1.,  1.]], requires_grad=True)


    tensor([[ 2.,  0.],
            [-2.,  2.]])



## Activation Functions

Sigmoid Activation: `nn.Sigmoid()`

ReLU Activation: `nn.ReLU()`

## Loss Functions
Mean Squared Error (for linear regression): `nn.MSELoss()`

Cross Entropy (for classification): `nn.CrossEntropyLoss()`

## Optimizer in `torch.optim`

Stochastic Gradient Descent (SGD): `torch.optim.SGD(params, lr, momentum = 0)`

where `params` refers to `model.parameters()`


# Define the Class

- Define our neural network by subclassing `nn.Module`
- Initialize the neural network layers in `__init__`. 
- Every `nn.Module` subclass implements the operations on input data in the `forward` method.
- More information see [Build the Neural Network](https://pytorch.org/tutorials/beginner/basics/buildmodel_tutorial.html#get-device-for-training)


```python
import torch.nn as nn
class MyModel(nn.Module):
    def __init__(self):
        super(MyModel, self).__init__() # 对继承自父类的属性进行初始化
        # 
        self.net = nn.Sequential(
            # 1 layer, 32 neuro
            nn.Linear(10, 32),
            nn.Sigmoid(),
            nn.Linear(32, 1))
    def forward(self, x):
        return self.net(x)
```

# Network Training
```python
dataset = MyDataset(file) # read data via MyDataset
# put dataset into Dataloader, 16 batches and get training set
tr_set = DataLoader(dataset, 16, shuffle=True) 
# contruct model and move to device (cpu/cuda)
model = MyModel().to(device) 
criterion = nn.MSELoss() # set loss function
optimizer = torch.optim.SGD(model.parameters(), 0.1) # set optimizer
```

```python
for epoch in range(n_epochs): # iterate n_epochs
    model.train() # set model to train mode
    
    # iterate through the dataloader
    for x, y in tr_set: 
        optimizer.zero_grad() # set gradient to zero
        x, y = x.to(device), y.to(device) # move data to device (cpu/cuda)
        pred = model(x) # forward pass (compute output)
        loss = criterion(pred, y) # compute loss
        loss.backward() # compute gradient (backpropagation)
        optimizer.step() # update model with optimizer
```

# Network Evaluation

## Validation Set

```python
model.eval() # set model to evaluation mode
total_loss = 0

# iterate through the dataloader
for x, y in dv_set:
    x, y = x.to(device), y.to(device)
    # disable gradient calculation
    with torch.no_grad():
        pred = model(x) # forward pass (compute output)
        loss = criterion(pred, y) # compute loss
    	total_loss += loss.cpu().item() * len(x) # accumulate loss
        avg_loss = total_loss / len(dv_set.dataset) # compute averaged loss

```

## Testing set

```python
model.eval() # set model to evaluation mode
preds = [] # define the epmty prediction list

# iterate through the dataloader
for x in tt_set:
    x = x.to(device) # move data to device
    # disable gradient calculation
    with torch.no_grad(): 
        pred = model(x) # forward pass (compute output)
        preds.append(pred.cpu()) # collect prediction

```

This notebook is based on [this ppt](https://1drv.ms/p/s!AhPTUXN0QjiSzQDCz7F2-bJePazg?e=ahvFET)
