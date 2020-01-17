# Notes 1/16,17/2020

## Finding:
 - ```Alley``` have a 93.77% and 92.67% missing rate in train and test sets. 
  - Droping ```Alley``` would properly be the best option
 - For some reason, there are more columns in the test set that have Nan.
 - ```FireplaceQu```*-Fireplace quality* is missing 47.26% and 50.03% values.
   - There is a 0.46 relationship between ```FireplaceQu``` and ```SalePrice```, however the corrlation graph droped all Nan for ```FireplaceQu```
-  ```Fence``` is missing 80.75% and 80.12% of its values
- Distrubition of ```SalePrice``` is skewed. 
  - Take the log of the price
## Encoding:
### Ordinal Categorical 
- There are 6 proberility of Fireplace ```[nan, 'TA', 'Gd', 'Po', 'Fa', 'Ex']```
  - [Meaning: ](https://books.google.com/books?id=CpGyDwAAQBAJ&pg=PA146&lpg=PA146&dq=%27TA%27,+%27Gd%27,+%27Po%27,+%27Fa%27,+%27Ex%27&source=bl&ots=5X0tpFoA8w&sig=ACfU3U07UiB_MNarL2KNq6FYXUHYerm95A&hl=en&sa=X&ved=2ahUKEwjgit7U44jnAhUNCs0KHb1_DagQ6AEwAXoECB0QAQ#v=onepage&q='TA'%2C%20'Gd'%2C%20'Po'%2C%20'Fa'%2C%20'Ex'&f=false)
 ```nan``` < ```Po```(Poor) < ```Fa```(Fair) < ```TA```(Typical) < ```Gd```(Good) < ```Ex```(Excellent)
- ```AlleyUnique``` 
  - ```nan``` < ```Grvl``` < ```Pave```
- ```StreetUnique```
  - ```Grvl``` < ```Pave```
- ```LandContourUnique```
  - ```Lvl```(Leveled), ```Bnk```(Banked), ```Low```(Depression), ```HLS```(Hillside)
  - Bnk/Low/HLS < Lvl
- ```Utilities```
  - ```NoSeWa``` < ```AllPub```
- ```LandSlope```
  - ```Sev``` (Severe) < ```Mod```(Moderate) < ```Gtl```(Gentle) 
- ```BldgType```
  - ```TwnhsI``` < ```TwnhsE``` < ```Duplx``` < ```2FmCon``` < ```1Fam```
- ```HouseStyle```
  - ```1Story``` < ```1.5Unf``` < ```1.5Fin``` < ```2Story```/```SFoyer```(Debatable) < ```2.5Unf``` < ```2.5Fin```

### Nominal Categorical
- ```Condition1```, ```Condition2```
  - ```['Norm','Feedr','PosN','Artery','RRAe','RRNn','RRAn','PosA','RRNe']```
  - 9 Uniques
- ```RoofStyle```
  - 6 Uniques
- ```RoofMatl```
  - 8 Uniques
- ```Exterior1st```, ```Exterior2nd```
  - ```['VinylSd','MetalSd','Wd Shng','HdBoard','Plywood','Wd Sdng','CmentBd','BrkFace','Stucco','AsbShng','Brk Cmn','ImStucc','AsphShn','Stone','Other','CBlock']```
  - 16 Uniques
- ```MasVnrType```
  - 5 Uniques
- 

## To-Do List:
- [ ] Draw a new corlation graph, where the distrubition is not skewed twords rows that have ```Alley``` and ```FireplaceQu```
- [ ] Drop ```Alley```
- [ ] Encode ```FireplaceQu``` with number
- [ ] Unskew ```SalePrice``` with log
- [ ] Encode
- [ ] Mean Code: 
  - [ ] ```YearBuilt```
  - [ ] ```YearRemodAdd```
