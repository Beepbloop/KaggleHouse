# KaggleHouse:  
My solution to Kaggle [House Prices: Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)  
---
## Data Processing and Feature Extration Approchs  
### **First Try:**  
 - One hot encoded all none neumerical features  
 - Included Nan in the encoding  
 - Filled all neumerical data Nans with means of the column  
### **Problems with this methods:**  
 - Data contains outliers  
 - Some numerical features are catergical  
 - Fill numerical data with means is not a good approch because: 
   - Numerical that contains ```Nan``` usualy becasue the house does not have this feature  
   - Outliers' effect the means greatly. 
 - Target collumn ```SalePrice``` is not in a normal disturbation. 
 - Data that are highly correlated (such as ```TotRmsAbvGrd``` and ```GrLivArea```)have repeted impact on the model  
    

## Model Approchs
  1. 
