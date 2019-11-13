# Kaggle - [House Prices: Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)  
---
## Data Processing and Feature Extration Approchs  
### **Data Processing 1:**  
 - One hot encoded all none neumerical features  
 - Included Nan in the encoding  
 - Filled all neumerical data Nans with means of the column  
 - Schewed Year data to be base on the minium of that column  
### **Problems:**  
 - Data contains outliers  
 - Some numerical features are catergical  
 - Fill numerical data with means is not a good approch because: 
   - Numerical that contains ```Nan``` usualy becasue the house does not have this feature  
   - Outliers' effect the means greatly. 
 - Target collumn ```SalePrice``` is not in a normal disturbation. 
 - Data that are highly correlated (such as ```TotRmsAbvGrd``` and ```GrLivArea```)have repeted impact on the model  
### **Data Processing 2:**  
 - One hot encoded all catergical
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
 ![](https://raw.githubusercontent.com/Beepbloop/KaggleHouse/master/NumericalDataDisturbitionGraph.png)The feature that have the highest corlation with ```SalePrice``` out of the two is removed. 
 - Fill all numerical feature Nan with 0
### **Data Processing 2:**  
*All creddit of this methods gose to [Golden](https://www.kaggle.com/goldens)'s [notebook](https://www.kaggle.com/goldens/house-prices-on-the-top-with-a-simple-model)*

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
 - Use 
 
