

[Statistics 507, Fall 2021](../index.html)
==========================================

#### Problem Set 5

#### Due Friday November 5 by 5pm.

Instructions
------------

Complete all questions of the assignment below and submit to Canvas by the due date. Remember, if you are using late days you should submit a draft of the assignment by the due date and leave a comment indicating how many late days you want to use.

For this problem set, you should submit source code as plain text Python scripts (with extension `.py`) and an associated Jupyter notebook (with extension `.ipynb`). Use [Jupytext](https://jupytext.readthedocs.io/en/latest/install.html) and (preferably) the _light_ format to associate the two files.

Questions on this and future problem sets may ask you to use concepts or ideas that have not been discussed in class. One of the goals of these assignments is to help you learn to be independent, read documentation, and otherwise make reasonable decisions about how to analyze and present data, code, or other data science material.

You may discuss the problem set and its solution with your peers, but you are required to work independently on the files to be submitted and to submit your own original work. If you use or closely follow patterns or code from sources other than the course notes or texts you should cite the source.

In addition to the content of your submission, you will be graded on the quality of your source code and the professionalism of your notebook file.

Maintain a consistent and literate style in your Python script and work to make your notebook look professional and well polished. Follow all style rules from previous problem sets.

When asked for a nicely formatted table you should produce one using HTML (perhaps via Markdown) and it should follow standards suitable for publication, e.g. columns should be named in English rather than `code_speak`. _Tables should also be produced using code_ so that minimal manual work would be needed to update the tables if the results were to change.

Question 0 - R-Squared Warmup \[20 points\]
-------------------------------------------

In this question you will fit a model to the ToothGrowth data used in the notes on [Resampling](https://jbhender.github.io/Stats507/F21/slides/resampling.slides.html) and [Statsmodels-OLS](https://jbhender.github.io/Stats507/F21/slides/statsmodels_ols.slides.html). Read the data, log transform tooth length, and then fit _a model_ with independent variables for supplement type, dose (as categorical), and their interaction. Demonstrate how to compute the R-Squared and Adjusted R-Squared values and compare your computations to the attributes (or properties) already present in the result object.

Question 1 - NHANES Dentition \[50 points\]
-------------------------------------------

In this question you will use the NHANES dentition and demographics data from problem sets 2 and 4.

1.  \[30 points\] Pick a single tooth (`OHXxxTC`) and model the probability that a permanent tooth is present (look up the corresponding statuses) as a function of age using logistic regression. For simplicity, assume the data are iid and ignore the survey weights and design. Use a [B-Spline](https://patsy.readthedocs.io/en/latest/spline-regression.html) basis to allow the probability to vary smoothly with age. Perform model selection using AIC or another method to choose the location of knots and the order of the basis (or just use `degree=3` (aka order) and focus on knots).
    
    Control for other demographics included in the data as warranted. You may also select these by minimizing AIC or you may choose to include some demographics regardless of whether they improve model fit. Describe your model building decisions and/or selection process and the series of models fit.
    
    **Update October 27:** When placing knots, be careful not to place knots at ages below (or equal to) the minimum age at which the tooth you are modeling is present in the data. Doing so will lead to an issue known as _perfect separation_ and make your model non-identifiable. To make the assignment easier you _may_ (but are not required to) limit the analyses to those age 12 and older and use no knots below age 14.
    
2.  \[10 points\] Fit the best model you find in part a to all other teeth in the data and create columns in your DataFrame for the fitted values.
    
    **Update October 27:** Leave the demographics alone, but if you are not restricting to those 12 and older you may need to modify the locations of the knots to make the models identifiable.
    
3.  \[10 points\] Create a visualization showing how the predicted probability that a permanent tooth is present varies with age for each tooth.
    

Question 2 - Hosmer-Lemeshow Calibration Plot \[30 points\]
-----------------------------------------------------------

In this question you will construct a plot often associated with the Hosmer-Lemeshow goodness-of-fit test. The plot is often used to assess the _calibration_ of a generalized linear models across the range of predicted values. Specifically, it is used to assess if the expected and observed means are approximately equal across the range of the expected mean.

Use the tooth you selected in question 1 part a for this question.

1.  Split the data into deciles based on the fitted (aka predicted) probabilities your model assigns to each subject’s tooth. The 10 groups you create using deciles should be approximately equal in size.
    
2.  Within each decile, compute the observed proportion of cases with a permanent tooth present and the expected proportion found by averaging the probabilities.
    
3.  Create a scatter plot comparing the observed and expected probabilities within each decile and add a line through the origin with slope 1 as a guide. Your model is considered well-calibrated if the points in this plot fall approximately on this line.
    
4.  Briefly comment on how-well calibrated your model is (or is not).
    
