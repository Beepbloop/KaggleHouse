# Kaggle Competition: [House Price Prediction](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)  
---  
## Data Processing and Feature Extration Approchs  
### **Data Processing 1:**  
 - Droped ```'Id'```
 - One hot encoded all none neumerical features  
 - Included Nan in the encoding  
 - Filled all neumerical data ```Nan``` with means of the column  
 - Schewed Year data to be base on the minium of that column  
### **Problems:**  
 - Data contains outliers  
 - Some numerical features are catergical  
 - Fill numerical data with means is not a good approch because: 
   - Numerical that contains ```Nan``` usualy becasue the house does not have this feature  
   - Outliers' effect the means greatly. 
 - Target collumn ```'SalePrice'``` is not in a normal disturbation. 
 - Data that are highly correlated have repeted impact on the model  
### **Data Processing 2:**  
 - One hot encoded all catergical features
 - Normoralized ```SalePrice``` distrubition to normal curve by taking  
 ```python
train['LogSalePrice'] = np.log(train['SalePrice'])
 ```
   Use
 ```python
train['SalePrice'] = np.exp(train['LogSalePrice'])
 ```
   to return to orignal distuibition
 - Reomved one feature from each set of features that have a corlation above 0.8, base on the disturbition graph. 
 ![](https://raw.githubusercontent.com/Beepbloop/KaggleHouse/master/NumericalDataDisturbitionGraph.png)The feature that have the highest corlation with ```'SalePrice'``` out of the two is removed. 
 - Fill all numerical feature Nan with 0
### **Data Processing 3:**  
*All creddit of this methods gose to [@Golden](https://www.kaggle.com/goldens) and her [notebook](https://www.kaggle.com/goldens/house-prices-on-the-top-with-a-simple-model)*  
 - Filled all numerical ```Nan``` with 0. 
 - Filled all categorical ```Nan``` with ```'None'```. 
 - Removed outliers recomended by author: 
 ```python
 train = train[train['GrLivArea']<4000]
 ```
 - Normoralized ```SalePrice``` 
 - One hot encoded all catergical features

## Model Approchs  
### **Linear Regression:**  
 - Used hyperparameter tuning to tune a sklearn linear regression model. 
 - Used polynomial features to expand feature space.
 - Use Root Mean Square Error ([RMSE](https://en.wikipedia.org/wiki/Root-mean-square_deviation)) as lost function since it is what the data is evluated by.  
 #### Result:  
 - First degree poly feature showed the best result
 - Optominal Alpha is less then 1000
 - Scores: 
   - Datas from 1: **0.24922**
   - Datas from 3: **0.31011**
### **Neural Network:**  
 - Implemented RMSE for both the default ```'SalePrice'``` and ```'LogSalePrice'```: 
 ```python
 def root_mean_squared_error(y_true, y_pred):
        return K.sqrt(K.mean(K.square(y_pred - y_true)))
 def exp_root_mean_squared_error(y_true, y_pred):
    return K.sqrt(K.mean(K.square(K.exp(y_pred)-K.exp(y_true))))
 ```
 - Established bsae line model: 
 ```_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
dense_1 (Dense)              (None, 512)               207872    
_________________________________________________________________
re_lu_1 (ReLU)               (None, 512)               0         
_________________________________________________________________
dense_2 (Dense)              (None, 512)               262656    
_________________________________________________________________
re_lu_2 (ReLU)               (None, 512)               0         
_________________________________________________________________
dense_3 (Dense)              (None, 512)               262656    
_________________________________________________________________
re_lu_3 (ReLU)               (None, 512)               0         
_________________________________________________________________
dense_4 (Dense)              (None, 1)                 513       
=================================================================
Total params: 733,697
Trainable params: 733,697
Non-trainable params: 0
_________________________________________________________________
```
   - 3 layers of 512 Dense ReLU neurons and one output neuron. 
   - Train untile ```'val_loss'``` stop increasing for 50 epochs. 
   - Default ```'adam'``` optimizer.  
   - RMSE ```root_mean_squared_error``` as loss. 
### Attempts:
 - Structurs:
   - Increase / Decrease neuron number of each layer
   - Increase / Decrease depths of the network
 - Activitation functions:
   - Sigmoid
   - Default LeakyReLU  ```alpha = 0.1```
   - LeakyReLU ```alpha = 0.5```
 - Optimizers:
   - Adam with increas / decrease learning rates
   - Default SGD
### Result:  
**Base Line Score: 0.21801**
 - Structurs：
   - Increasing model size and num of neurons resulted in the exact same score,
   - Decreasing it result in sigenfigent score 
 - Activitation functions:
   - Sigmoid did not converge under 10000 epochs. 
   - Default LeakyReLU resulted in slightly better score: **0.21259**
   - LeakyReLU with ```alpha = 0.5``` performed less then default, scored: **0.21337**  
 - Optimizer:
   - Most optomal Adam ```learning_rate = 0.0001```,scored of **0.21106**
   - SGD did not converge under 10000 epochs.
 - Combined Model:
   - **Parameters:** Defalut LeakyReLU, Adam ```learning_rate = 0.0001```, 3 layers of 521 neurons.
   - **Score:** 0.21406, some how a combenation of these has increased the score. 
### Lasso Regression
*This approch is build upon [@Golden](https://www.kaggle.com/goldens)'s [notebook](https://www.kaggle.com/goldens/house-prices-on-the-top-with-a-simple-model)*  
 - Used hyperparameter to turn a Lasso Regression model
 - Golden's Parameter
### Result: 
 - Golden's Score: **0.11888**
 - Hyper tuned best paramete 
 ```python
 Lasso(alpha = 0.0005, fit_intercept = True, normalize = False)
 ```
   - Score: **0.11744**
