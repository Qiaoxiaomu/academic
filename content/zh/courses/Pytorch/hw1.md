---
date: "2021-03-10"
title: 02 Homework 1 Regression
subtitile: COVID-19 Cases Prediction
type: book
weight: 2
---

>This document is based on the homework 1 (COVID-19 Cases Prediction) of Machine Learning 2021 given by Hung-yi Lee from Nation Taiwan University. I tried to dompose the sample code and give more helpful comments. I'll also give my solution to the homework. 

>The [homework description](https://speech.ee.ntu.edu.tw/~hylee/ml/ml2021-course-data/hw/HW01/HW01.pdf) and [sample code](https://colab.research.google.com/github/ga642381/ML2021-Spring/blob/main/HW01/HW01.ipynb) can be found from the [github source](https://github.com/ga642381/ML2021-Spring/tree/main/HW01).
>You can download data from [kaggle](https://www.kaggle.com/c/ml2021spring-hw1/data), and upload data manually to the workspace to see performance (5 times per day).

# Data Prepocessing

## Data Description

We have three kinds of datasets:
* `train`: for training, including 93 features and 1 target in total
* `dev`: for validation, including 93 featrues and 1 target in total
* `test`: for testing, including 93 features, no target value so that we need to predict it.


```python
# show the covid.training.csv
import pandas as pd
train = pd.read_csv("covid.train.csv").set_index("id")
train.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AL</th>
      <th>AK</th>
      <th>AZ</th>
      <th>AR</th>
      <th>CA</th>
      <th>CO</th>
      <th>CT</th>
      <th>FL</th>
      <th>GA</th>
      <th>ID</th>
      <th>...</th>
      <th>restaurant.2</th>
      <th>spent_time.2</th>
      <th>large_event.2</th>
      <th>public_transit.2</th>
      <th>anxious.2</th>
      <th>depressed.2</th>
      <th>felt_isolated.2</th>
      <th>worried_become_ill.2</th>
      <th>worried_finances.2</th>
      <th>tested_positive.2</th>
    </tr>
    <tr>
      <th>id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>23.812411</td>
      <td>43.430423</td>
      <td>16.151527</td>
      <td>1.602635</td>
      <td>15.409449</td>
      <td>12.088688</td>
      <td>16.702086</td>
      <td>53.991549</td>
      <td>43.604229</td>
      <td>20.704935</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>23.682974</td>
      <td>43.196313</td>
      <td>16.123386</td>
      <td>1.641863</td>
      <td>15.230063</td>
      <td>11.809047</td>
      <td>16.506973</td>
      <td>54.185521</td>
      <td>42.665766</td>
      <td>21.292911</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>23.593983</td>
      <td>43.362200</td>
      <td>16.159971</td>
      <td>1.677523</td>
      <td>15.717207</td>
      <td>12.355918</td>
      <td>16.273294</td>
      <td>53.637069</td>
      <td>42.972417</td>
      <td>21.166656</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>22.576992</td>
      <td>42.954574</td>
      <td>15.544373</td>
      <td>1.578030</td>
      <td>15.295650</td>
      <td>12.218123</td>
      <td>16.045504</td>
      <td>52.446223</td>
      <td>42.907472</td>
      <td>19.896607</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>22.091433</td>
      <td>43.290957</td>
      <td>15.214655</td>
      <td>1.641667</td>
      <td>14.778802</td>
      <td>12.417256</td>
      <td>16.134238</td>
      <td>52.560315</td>
      <td>43.321985</td>
      <td>20.178428</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 94 columns</p>
</div>



## Dataset


```python
import numpy as np
import csv

import torch
from torch.utils.data import Dataset, DataLoader
```


```python
class COVID19Dataset(Dataset):
    ''' Dataset for loading and preprocessing the COVID19 dataset '''
    def __init__(self,
                 path,
                 mode='train',
                 target_only=False):
        self.mode = mode

        # Read data into numpy arrays
        with open(path, 'r') as fp:
            data = list(csv.reader(fp))
            data = np.array(data[1:])[:, 1:].astype(float) # don't include the first id col

        # Features seletcion
        if not target_only:
            # 40 + 18 + 18 + 17 = 93 features
            feats = list(range(93))
        else:
            # TODO: Using 40 states & 2 tested_positive features (indices = 57 & 75)
            feats = list(range(40))
            feats.append(57)
            feats.append(75)
        # test set has no target, train & dev sets have target    
        if mode == 'test':
            # Testing data
            # data: 893 x 93 (40 states + day 1 (18) + day 2 (18) + day 3 (17))
            data = data[:, feats]
            self.data = torch.FloatTensor(data)
        else:
            # Training data (train/dev sets)
            # data: 2700 x 94 (40 states + day 1 (18) + day 2 (18) + day 3 (18))
            target = data[:, -1] # the last col is the target col
            data = data[:, feats] # the first 93 cols are the features
            
            # Splitting training data into train & dev sets
            # Select samples whose ids are multiples of 10 as dev sets
            if mode == 'train':
                indices = [i for i in range(len(data)) if i % 10 != 0]
            elif mode == 'dev':
                indices = [i for i in range(len(data)) if i % 10 == 0]
            
            # Convert data into PyTorch tensors
            self.data = torch.FloatTensor(data[indices])
            self.target = torch.FloatTensor(target[indices])

        # Normalize features (you may remove this part to see what will happen)
        self.data[:, 40:] = \
            (self.data[:, 40:] - self.data[:, 40:].mean(dim=0, keepdim=True)) \
            / self.data[:, 40:].std(dim=0, keepdim=True)

        self.dim = self.data.shape[1]

        print('Finished reading the {} set of COVID19 Dataset ({} samples found, each dim = {})'
              .format(mode, len(self.data), self.dim))

    def __getitem__(self, index):
        # Returns one sample at a time
        if self.mode in ['train', 'dev']:
            # For training (with target)
            return self.data[index], self.target[index]
        else:
            # For testing (no target)
            return self.data[index]

    def __len__(self):
        # Returns the size of the dataset
        return len(self.data)
```

## Dataloader

A `DataLoader` loads data from a given `Dataset` into batches.

Remember that if `target_only=False`, then there are 93 features used in training.


```python
def prep_dataloader(path, mode, batch_size, n_jobs=0, target_only=False):
    ''' Generates a dataset, then is put into a dataloader. '''
    dataset = COVID19Dataset(path, mode=mode, target_only=target_only)  # Construct dataset
    dataloader = DataLoader(
        dataset, batch_size,
        shuffle=(mode == 'train'), drop_last=False,
        num_workers=n_jobs, pin_memory=True)                            # Construct dataloader
    return dataloader
```

## Load Data

`config` is a dic about the hyper parameters setting which will be seen later.


```python
tr_set = prep_dataloader(tr_path, 'train', config['batch_size'], target_only=target_only)
dv_set = prep_dataloader(tr_path, 'dev', config['batch_size'], target_only=target_only)
tt_set = prep_dataloader(tt_path, 'test', config['batch_size'], target_only=target_only)
```

# Network Building

## Network

`NeuralNet` is an `nn.Module` designed for regression. The DNN consists of 2 fully-connected layers with ReLU activation. This module also included a function `cal_loss` for calculating loss.



```python
import torch
import torch.nn as nn
class NeuralNet(nn.Module):
    ''' A simple fully-connected deep neural network '''
    def __init__(self, input_dim):
        super(NeuralNet, self).__init__()

        # Define your neural network here
        # TODO: How to modify this model to achieve better performance?
        self.net = nn.Sequential(
            nn.Linear(input_dim, 64),
            nn.ReLU(),
            nn.Linear(64, 1)
            )
        # Mean squared error loss
        self.criterion = nn.MSELoss(reduction='mean')

    def forward(self, x):
        ''' Given input of size (batch_size x input_dim), compute output of the network '''
        return self.net(x).squeeze(1)

    def cal_loss(self, pred, target):
        ''' Calculate loss '''
        # TODO: you may implement L2 regularization here
        # one possible l2 regularization will be given in Solution part
        return self.criterion(pred, target)
```


```python
model = NeuralNet(tr_set.dataset.dim).to(device)  # Construct model and move to device
```

## Setup Hyper-parameters
`config` contains hyper-parameters for training and the path to save your model.

Since different optimizer has different kinds and numbers of hyper-parameters, it's better to put them together in config as `optim_hyparas`, which is easier to invoke


```python
def get_device():
    ''' Get device (if GPU is available, use GPU) '''
    return 'cuda' if torch.cuda.is_available() else 'cpu'
```


```python
device = get_device()                 # get the current available device ('cpu' or 'cuda')
os.makedirs('models', exist_ok=True)  # The trained model will be saved to ./models/
target_only = False                   # TODO: Using 40 states & 2 tested_positive features

# TODO: How to tune these hyper-parameters to improve your model's performance?
config = {
    'n_epochs': 3000,                # maximum number of epochs
    'batch_size': 270,               # mini-batch size for dataloader
    'optimizer': 'SGD',              # optimization algorithm (optimizer in torch.optim)
    'optim_hparas': {                # hyper-parameters for the optimizer (depends on which optimizer you are using)
        'lr': 0.001,                 # learning rate of SGD
        'momentum': 0.9              # momentum for SGD
    },
    'early_stop': 200,               # early stopping epochs (the number epochs since your model's last improvement)
    'save_path': 'models/model.pth'  # your model will be saved here
}
```

# Train, Validate, Predict

## Training

This function is used to train the model and get the training loss. An early-stop mechanism is applied.

```python
def train(tr_set, dv_set, model, config, device):
    ''' DNN training '''

    n_epochs = config['n_epochs']  # Maximum number of epochs

    # Setup optimizer
    # optimizer = torch.optim.config['optimizer']
    optimizer = getattr(torch.optim, config['optimizer'])(
        model.parameters(), **config['optim_hparas'])

    min_mse = 1000.
    loss_record = {'train': [], 'dev': []}      # for recording training loss
    early_stop_cnt = 0
    epoch = 0
    while epoch < n_epochs:
        model.train()                           # set model to training mode
        for x, y in tr_set:                     # iterate through the dataloader
            optimizer.zero_grad()               # set gradient to zero
            x, y = x.to(device), y.to(device)   # move data to device (cpu/cuda)
            pred = model(x)                     # forward pass (compute output)
            mse_loss = model.cal_loss(pred, y)  # compute loss
            mse_loss.backward()                 # compute gradient (backpropagation)
            optimizer.step()                    # update model with optimizer
            loss_record['train'].append(mse_loss.detach().cpu().item())

        # After each epoch, test your model on the validation (development) set.
        dev_mse = dev(dv_set, model, device)
        if dev_mse < min_mse:
            # Save model if your model improved
            min_mse = dev_mse
            print('Saving model (epoch = {:4d}, loss = {:.4f})'
                .format(epoch + 1, min_mse))
            torch.save(model.state_dict(), config['save_path'])  # Save model to specified path
            early_stop_cnt = 0
        else:
            early_stop_cnt += 1

        epoch += 1
        loss_record['dev'].append(dev_mse)
        if early_stop_cnt > config['early_stop']:
            # Stop training if your model stops improving for "config['early_stop']" epochs.
            break

    print('Finished training after {} epochs'.format(epoch))
    return min_mse, loss_record
```

## Validation

This function is used to to get the loss on the dev set. 

```python
def dev(dv_set, model, device):
    model.eval()                                # set model to evalutation mode
    total_loss = 0
    # x is the feature vector, y is target
    for x, y in dv_set:                         # iterate through the dataloader
        x, y = x.to(device), y.to(device)       # move data to device (cpu/cuda)
        with torch.no_grad():                   # disable gradient calculation
            pred = model(x)                     # forward pass (compute output)
            mse_loss = model.cal_loss(pred, y)  # compute loss
        total_loss += mse_loss.detach().cpu().item() * len(x)  # accumulate loss
    total_loss = total_loss / len(dv_set.dataset)              # compute averaged loss

    return total_loss
```

## Testing

This function is used for getting the prediciton of the test data.

```python
def test(tt_set, model, device):
    model.eval()                                # set model to evalutation mode
    preds = []                                  # for saving predictions
    for x in tt_set:                            # iterate through the dataloader
        x = x.to(device)                        # move data to device (cpu/cuda)
        with torch.no_grad():                   # disable gradient calculation
            pred = model(x)                     # forward pass (compute output)
            preds.append(pred.detach().cpu())   # collect prediction
    preds = torch.cat(preds, dim=0).numpy()     # concatenate all predictions and convert to a numpy array
    return preds
```

# Solution

## Midium Baseline

According to the hints given by the TA, we may achieve midium baseline by feature selection, i.e., by finishing `TODO` in `COVID19Dataset`. One possible solution is given below. (Kaggle test score 1.0380)


```python
class COVID19Dataset(Dataset):
    ''' Dataset for loading and preprocessing the COVID19 dataset '''
    def __init__(self,
                 path,
                 mode='train',
                 target_only=False):
        self.mode = mode

        # Read data into numpy arrays
        with open(path, 'r') as fp:
            data = list(csv.reader(fp))
            data = np.array(data[1:])[:, 1:].astype(float) # don't include the first id col
        
        if not target_only:
            # 40 + 18 + 18 + 17 = 93 features
            feats = list(range(93))
        else:
            # TODO: Using 40 states & 2 tested_positive features (indices = 57 & 75)
            feats = list(range(40))
            feats.append(57)
            feats.append(75)
```

## Strong Baseline
The TA mentions 5 hints about stron baseline:
* Feature selection (what other features are useful?)
* DNN architecture (layers? dimension? activation function?)
* Training (mini-batch? optimizer? learning rate?)
* L2 regularization
* There are some mistakes in the sample code, can you find them?

I've tried some of them, unluckilly the performance is not better than the midium baseline. Anyway, I still give my possible solutions to L2 regularization and one possible mistake I found in the sample code.

**DNN architecture**

I've tried some models like below, but the performance hasn't been promoted. I guess it results from the unproper hyper-parameters tuning.


```python
class NeuralNet(nn.Module):
    ''' A simple fully-connected deep neural network '''
    def __init__(self, input_dim):
        super(NeuralNet, self).__init__()

        # Define your neural network here
        # TODO: How to modify this model to achieve better performance?
        self.net = nn.Sequential(
            nn.Linear(input_dim, 8),
            nn.ReLU(),
            nn.Linear(8, 8),
            nn.ReLU(),
            nn.Linear(8, 1)
            )
        # Mean squared error loss
        self.criterion = nn.MSELoss(reduction='mean')
```

**L2 regularization**

Chanege the `cal_loss` method in class `NeuralNet` to the given code.


```python
def cal_loss(self, pred, target):
    ''' Calculate loss '''
    # TODO: you may implement L2 regularization here
    l2 = 0
    for i in model.state_dict():
        if i[-6:] == "weight": # only use weight params to do l2
            l2 += model.state_dict()[i].pow(2).sum()
    # float(0.001 * l2) is the penalty term and 0.001 can be adjusted
    return self.criterion(pred, target) + float(0.001 * l2)
```

**One possible mistake**

If you run the sample code directly, you'll find that the output `pred.csv` has a null line between 2 sequential rows. This can be worked out by changing `save_pred` function, simply by adding `newline=''`.


```python
with open(file, 'w', newline='') as fp:
        writer = csv.writer(fp)
        writer.writerow(['id', 'tested_positive'])
        for i, p in enumerate(preds):
            writer.writerow([i, p])
```

# Statement

The sample code is completely written by [Heng-Jui Chang @ NTUEE](https://github.com/ga642381/ML2021-Spring/blob/main/HW01/HW01.ipynb). 

The possible solution is written by [Hanyu Zheng](nickzhy.com).

Copying or reusing requires to specify the original author. You shall not use my solution as your homework directly.
