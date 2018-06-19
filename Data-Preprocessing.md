#### You can get back to the main page

# [Here](https://github.com/Lexscher/Machine_Learning/blob/master/README.md)

---

## Get the dataset

So, Right off the bat, we're given a dataset about customers. This has four columns:
Country, Age, Salary, & Purchased (I _guess_ this is a [(string/varchar), integer, integer, boolean] kind of situation. Dunno, could be wrong!), with ten rows.

The first three columns are _Independent Variabls_ whereas the last column is a _Dependent Variable_. The goal is to use the information from _independent variables_ to predict the outcome/value of _dependent variables_.

## Importing the libraries

There are three libraries that we'll most likely import each time we start a project:

1.  numpy - helps us with math & calculations
2.  matplotlib - helps us plot charts
    (However, we'll key into the extension with dot notation)
    matplotlib.pyplot
3.  pandas - helps us with dataset importing & management

##### With R, the libraries are already imported, so we're good on that part. Just hit the _*packages*_ tab, and we'll see a list of all of our available libraries.

## Importing the datasets

##### Python

We can use the file to set our working directory. We'll look into the directory that contains our Data.csv file, using the File Explorer. Then we press Run🏃‍♀️🏃‍♂️!

Then we can import the files.

Here's an example of importing the first three columns of the dataset:
![import datasets 2](https://github.com/Lexscher/Machine_Learning/blob/master/Images/import_datasets2.png)

![import datasets](https://github.com/Lexscher/Machine_Learning/blob/master/Images/import_datasets1.png)

##### R

It's a tad simpler! We won't have to worry about making a distinction between the matrix of features and the dependent variable vector.

We'll find the directory that contains our Data.csv file, and set _that_ as our working directory. Then, in the "console" pane, we'll write:

```
 dataset = read.csv('Data.csv')
```

After we run this, we'll see the the dataset in the environment pane:

![import datasets(R)](https://github.com/Lexscher/Machine_Learning/blob/master/Images/import_datasets_R1.png)

Then, all you have to do is click on it:

![import datasets](https://github.com/Lexscher/Machine_Learning/blob/master/Images/import_datasets_R2.png)

---

_Before we start the "Missing Data" lesson, Hadelin gives us a brief summary of classes, objects, and methods. If you're already familiar with these topics, you can just skip ahead. It's good for those who are following the Python section with no prior experience in object-oriented programming._

## Missing data

If we take a closer look at the dataset, we'll notice that the customer from _Spain_ has missing data in the _Age_ column, and the customer from _Germany_ has no data in the _Salary_ column.

A common practice where missing data is concerned: Replace the missing data with the _mean_ of the values in that same column.

-   _The mean of all the values in the *Age* column will become the value of the missing data in the column where the customer is from *Spain*_

##### Python

_Note:_ _If you can't see the full array, run_

```py
 np.set_printoptions(threshold = np.nan)
```

---

So, we'll import a library to do get the mean instead of creating a method, ourselves.

```py
from sklearn.preprocessing import Imputer
```

Use _command + I_ in front of a to use the Object Inspector (_\_Which is now the "Help" tab)_

If you'd like to know more about Scikit Learn, you can go _[here](http://scikit-learn.org/stable/index.html)_.

This was the process to handle the missing data.

```py
# Handling the missing data
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
imputer = imputer.fit(X[:, 1:3])
X[:, 1:3] = imputer.transform(X[:, 1:3])
# The reason we do [:, 1:3] and not [:, 1:2] is because the upper bound is not included, while the lower bound is included.
```

The object inspector gave us information about the parameters of the Imputer method (missing*values, strategy, axis, verbose, & copy). We used the parameters that were necessary (missing_values, strategy, & axis).
The *missing*values* param can be assigned a value that's an \_integer* or \_NaN*.
The _strategy_ param can be assigned a string value, _'mean', 'median', or 'most_frequent'_(imputation strategies).
The _axis_ param can be assigned a value that's an _integer_, _0 or 1_ (The axis along which to impute).

The _Age_, _NaN_, becomes _*38.77777777777778*_, and the _Salary_, _NaN_, becomes _*63777.77777777778*_.

If we just enter "X" in the console, the new dataset will have the values we received by using the Imputer method.

![Missing Values Python](https://github.com/Lexscher/Machine_Learning/blob/master/Images/missing_data_Py.png)

##### R

This shall be relatively similar to what we did using Python, however, we'll have to handle the pieces of missing data separately.

Age:

```
dataset$Age = ifelse(is.na(dataset$Age),
                     ave(dataset$Age, FUN = function(x) mean(x,  na.rm = TRUE)),
                     dataset$Age)
```

Salary:

```
dataset$Salary = ifelse(is.na(dataset$Salary),
                        ave(dataset$Salary, FUN = function(x) mean(x,  na.rm = TRUE)),
                        dataset$Salary)
```

In ifelse, the first parameter is the condition, the second parameter is the value you want to input if the condition is true, and the third parameter is the value you want to input if the condition is false.

_is.na_ is a function that tells us if the value is missing, so this...

```
is.na(dataset$Salary)
```

... will return true if any value of the column, Salary, is missing and false if a value in the column, Salary, is not missing.
In the next parameter:

```
ave(dataset$Salary, FUN = function(x) mean(x,  na.rm = TRUE))
```

We use the method, ave, which takes the column, Salary, and gets the average of all the present values, then a function, which uses the method, mean, as a callback.

-   which will take that missing value, x, and replace it with the mean of all the values in the column, Salary.

The third parameter:

```
dataset$Salary
```

Just tells us when the value in the column, Salary, is _not_ missing, we'll just keep that value (we won't change anything here).

When we command enter these lines, and check our dataset, we'll see that the missing values were in fact replaced with the average of their columns:

![Missing Values R](https://github.com/Lexscher/Machine_Learning/blob/master/Images/missing_data_R.png)

---

## Categorical Data

If we take a closer look at our dataset, we'll see that there are two columns that contain data that can be categorized.

The Country column contains 3 categories:
France
Spain
Germany

The Purchased column contains 2 categories:
Yes
No

What we're going to do is _encode_ our _text_ variables into _numbers_, because machine learning models are based on mathematical equations.

You may notice that the methods we use in Python are quite different from the methods we use in R.

##### Python

We'll have to import the method, _*LabelEncoder*_, that will help us encode our categorical data. We get this from our friendly neighborhood sklearn.

```py
from sklearn.preprocessing import LabelEncoder
labelencoder_X = LabelEncoder()
X[:, 0] = Xlabelencoder_X.fit_transform(X[:, 0])
```

So, we applied the LabelEncoder to all rows (X[*:*_..._) in the the first column( _..._, *0*]).
![encoding categorical data: Python](https://github.com/Lexscher/Machine_Learning/blob/master/Images/encoding_categorical_data_Py.png)

But, there may be a problem with this method. When we do this, Python will think Spain is greater than Germany & France, and Germany is greater than France.
Since we don't want our column's items to have this kind of relationship with one another, we'll import another, called _*OneHotEncoder*_

```py
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[:, 0] = Xlabelencoder_X.fit_transform(X[:, 0])
onehotencoder = OneHotEncoder(categorical_features = 0)
X = onehotencoder.fit_transform(X).toarray()
```

##### R

---

## Splitting the Dataset into the Training set and Test set

##### Python

##### R

---

## Feature Scaling

##### Python

##### R

---

## Data Preprocessing Template
