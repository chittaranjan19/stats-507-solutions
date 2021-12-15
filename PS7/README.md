

[Statistics 507, Fall 2021](../index.html)
==========================================

#### Problem Set 7

#### Due Tuesday November 23 by 5pm.

Instructions
------------

Complete all questions of the assignment below and submit to Canvas by the due date. Remember, if you are using late days you should submit a draft of the assignment by the due date and leave a comment indicating how many late days you want to use.

For this problem set, you should submit source code as a plain text _markdown_ script (with extension `.md`) and an associated Jupyter notebook (with extension `.ipynb`). Use [Jupytext](https://jupytext.readthedocs.io/en/latest/install.html) to associate the two files.

Questions on this and future problem sets may ask you to use concepts or ideas that have not been discussed in class. One of the goals of these assignments is to help you learn to be independent, read documentation, and otherwise make reasonable decisions about how to analyze and present data, code, or other data science material.

You may discuss the problem set and its solution with your peers, but you are required to work independently on the files to be submitted and to submit your own original work. If you use or closely follow patterns or code from sources other than the course notes or texts you should cite the source.

In addition to the content of your submission, you will be graded on the quality of your source code and the professionalism of your notebook file.

Maintain a consistent and literate style in your markdown script and work to make your notebook look professional and well polished. Follow all style rules from previous problem sets.

_Note:_ For this assignment only, you may use two late days to extend the due date to Monday November 29 by 5pm.

Question 0 - Data Prep \[10 points\]
------------------------------------

In this problem set you will train and tune machine learning _regression_ models for a [Superconductivty](https://archive.ics.uci.edu/ml/datasets/Superconductivty+Data) dataset. In this dataset the goal is to predict the critical temperature based on 81 features extracted from a chemical formula of a material. You should use mean squared error (or an equivalent) as the loss function.

In this question you will prepare the data for training and tuning models in the following question. To do so, read the data into Python and create DataFrames or Numpy arrays for the features and dependent regression target (critical temperature).

Then, split the cases into three parts: use 80% of the cases for training, hold 10% for validation and model comparison in question 2, and reserve 10% as a test dataset.

Question 1 - Training and Tuning Models \[70 points\]
-----------------------------------------------------

In this question you should train and tune elastic-net, random forest, and gradient boosted decision tree models using the 80% training sample from question 0. Tune hyper-parameters for each model class using 10-fold cross-validation.

### part a

Train a series of elastic net models and choose the mixing parameter `l1_ratio` and the amount of regularization `C` using 10-fold cross-validation over a grid (or grids) of values.

Create a figure or table showing the cross-validated MSE at key points in your grid and identity which hyper-parameters minimize this quantity.

### part b

Train a series of random forest models and use 10-fold cross-validation for hyper-parameter selection. Focus on tuning the tree depth and number of trees. You may, but are not required, to tune other hyper-parameters as well.

Create a figure or table showing the cross-validated MSE for different hyper-parameters considered and identity which hyper-parameters minimize this quantity.

### part c

Train a series of gradient boosted tree models and use 10-fold cross-validation for hyper-parameter selection. Focus on tuning the number of boosting rounds after selecting a suitable learning rate. You may, but are not required, to t une other hyper-parameters as well.

Create a figure or table showing how the cross-validated MSE changes with the the number of boosting rounds and identity which hyper-parameters minimize this quantity.

Question 2 - Validation and Testing \[20 points\]
-------------------------------------------------

Using the hyperparameter selected in the previous section, train 3 models - one for each class - on the entire training sample. (You can do this in the previous question for elastic net.)

Use the trained models to make predictions for each case in the validation set created in question 0. Create a nicely formatted table comparing the out-of-sample MSE on the validation dataset for these three models.

Use whichever model performs best in terms of MSE on the validation dataset to make predictions on the test data and report the corresponding MSE.

