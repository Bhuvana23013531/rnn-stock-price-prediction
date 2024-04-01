# Stock Price Prediction
### NAME: BHUVANESHWARI M
### REGISTER NUMBER: 212223230033
## AIM

To develop a Recurrent Neural Network model for stock price prediction.

## Problem Statement and Dataset
Make a Recurrent Neural Network model for predicting stock price using a training and testing dataset. The model will learn from the training dataset sample and then the testing data is pushed for testing the model accuracy for checking its accuracy. The Dataset has features of market open price, closing price, high and low price for each day.

![Screenshot 2024-04-01 141814](https://github.com/Bhuvana23013531/rnn-stock-price-prediction/assets/147125678/4f7888ae-477d-474e-bada-e87c7fbfa6e9)


## DESIGN STEPS

### STEP 1:
Import necessary libraries.
### STEP 2:
Load the dataset.
### STEP 3:
Create the model and compile.
### STEP 4:
Fit the model. Evaluate the model.

## PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from sklearn.preprocessing import MinMaxScaler
from keras import layers
from keras.models import Sequential
dataset_train = pd.read_csv('trainset.csv')
dataset_train.head()
train_set = dataset_train.iloc[:,1:2].values
type(train_set)
train_set.shape
sc = MinMaxScaler(feature_range=(0,1))
training_set_scaled = sc.fit_transform(train_set)
training_set_scaled.shape
X_train_array = []
y_train_array = []
for i in range(60, 1259):
  X_train_array.append(training_set_scaled[i-60:i,0])
  y_train_array.append(training_set_scaled[i,0])
X_train, y_train = np.array(X_train_array), np.array(y_train_array)
X_train1 = X_train.reshape((X_train.shape[0], X_train.shape[1],1))
X_train.shape
length = 60
n_features = 1
model = Sequential()
model.add(layers.SimpleRNN(50,input_shape=(60,1)))
model.add(layers.Dense(1))
model.compile(optimizer='adam', loss='mse')
model.summary()
model.fit(X_train1,y_train,epochs=100, batch_size=32)
dataset_test = pd.read_csv('testset.csv')
test_set = dataset_test.iloc[:,1:2].values
test_set.shape
dataset_total = pd.concat((dataset_train['Open'],dataset_test['Open']),axis=0)
inputs = dataset_total.values
inputs = inputs.reshape(-1,1)
inputs_scaled=sc.transform(inputs)
X_test = []
for i in range(60,1384):
  X_test.append(inputs_scaled[i-60:i,0])
X_test = np.array(X_test)
X_test = np.reshape(X_test,(X_test.shape[0], X_test.shape[1],1))
X_test.shape
predicted_stock_price_scaled = model.predict(X_test)
predicted_stock_price = sc.inverse_transform(predicted_stock_price_scaled)
plt.plot(np.arange(0,1384),inputs, color='red', label = 'Test(Real) Google stock price')
plt.plot(np.arange(60,1384),predicted_stock_price, color='black', label = 'Predicted Google stock price')
plt.title('Google Stock Price Prediction')
plt.xlabel('Time')
plt.ylabel('Google Stock Price')
plt.legend()
plt.show()
```
## OUTPUT

### True Stock Price, Predicted Stock Price vs time
![Screenshot 2024-04-01 142029](https://github.com/Bhuvana23013531/rnn-stock-price-prediction/assets/147125678/1be589f2-c3e2-4f2e-8ac8-4f18b40fcf2d)


### Mean Square Error
![Screenshot 2024-04-01 142112](https://github.com/Bhuvana23013531/rnn-stock-price-prediction/assets/147125678/594d19d7-f90b-43a9-86e0-a615018b3555)


## RESULT
A Recurrent Neural Network model for stock price prediction is developed.
