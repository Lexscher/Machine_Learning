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
