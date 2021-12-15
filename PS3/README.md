
[Statistics 507, Fall 2021](../index.html)
==========================================

#### Problem Set 3

#### Due Friday October 8 by 5pm.

Instructions
------------

Complete all questions of the assignment below and submit to Canvas by the due date. Remember, if you are using late days you should submit a draft of the assignment by the due date and leave a comment indicating how many late days you want to use.

For this problem set, you should submit source code as plain text Python scripts (with extension `.py`) and an associated Jupyter notebook (with extension `.ipynb`). Use [Jupytext](https://jupytext.readthedocs.io/en/latest/install.html) and (preferably) the _light_ format to associate the two files.

Questions on this and future problem sets may ask you to use concepts or ideas that have not been discussed in class. One of the goals of these assignments is to help you learn to be independent, read documentation, and otherwise make reasonable decisions about how to analyze and present data, code, or other data science material.

You may discuss the problem set and its solution with your peers, but you are required to work independently on the files to be submitted and to submit your own original work. If you use or closely follow patterns or code from sources other than the course notes or texts you should cite the source.

In addition to the content of your submission, you will be graded on the quality of your source code and the professionalism of your notebook file.

Maintain a consistent and literate style in your Python script and work to make your notebook look professional and well polished. Follow all style rules from previous problem sets. Here are 3 additional style rules focused on naming and indentation you should follow to receive full credit:

1.  Name all variables using all lower-case,
2.  Use `snake_case` for variable names with multiple words,
3.  When chaining 3 or more method calls, put each on its own line with leading periods aligned. (You _may_ but are _not required_ to do this for fewer method calls).

When asked for a nicely formatted table you should produce one using HTML (perhaps via Markdown) and it should follow standards suitable for publication, e.g. columns should be named in English rather than `code_speak`. _Tables should also be produced using code_ so that minimal manual work would be needed to update the tables if the results were to change.

**Addendum** (October 5): You may have Markdown lines longer than 79 characters for long URLS if you use _reference style_ links.

Question 0 - RECS and Replicate Weights \[15 points\]
-----------------------------------------------------

In this problem set, you will analyze data from the 2009 and 2015 Residential Energy Consumption Surveys [RECS](https://www.eia.gov/consumption/residential/) put out by the US Energy Information Agency. In this warm up question, you will:

*   find URLs from which to download the data for subsequent questions,
*   determine variables you will need by examining the code-books, and  
    
*   familiarize yourself with the replicate weight method used for computing standard errors and constructing confidence intervals.

### Data Files

Find links to the 2009 and 2015 [RECS](https://www.eia.gov/consumption/residential/) micro-data files and report them here. In the 2009 data year the replicate weights (see below) are distributed in a separate file. Find and report the link to that file as well.

### Variables

Using the code-books for the associated data files, determine what variables you will need to answer the following question. Be sure to include variables like the unit id and sample weights.

> Estimate the average number of heating and cooling degree days (base temperature 65 °F) for residences in each Census region for both 2009 and 2015.

### Weights and Replicate Weights

Residences participating in the RECS surveys are not an independent and identically distributed sample of residences from the population of all US residences in the survey years. Instead, a complex sampling procedure is used. The details of the sampling process are beyond the scope of this course and assignment. However, you do need to know that residences in the surveys are _weighted_ and to make use of those weights in your solution. Moreover, these surveys include _balanced repeated replicate_ (brr) _weights_ to facilitate computation of standard errors and, in turn, construction of confidence intervals.

On the same page as the data, you will find a link explaining how to use the replicate weights. Report that link here; then, citing the linked document, briefly explain how the replicate weights are used to estimate standard errors for weighted point estimates. The _standard error of an estimator_ is the _square root_ of that estimator’s _variance_. Please note that I am asking you about the _standard error_ and not the _relative_ standard error. In your explanation please retype the key equation making sure to document what each variable in the equation is. Don’t forget to include the _Fay coefficient_ and its value(s) for the specific replicate weights included with the survey data.

Question 1 - Data Preparation \[20 points\]
-------------------------------------------

In this question you will use Pandas to download, read, and clean the RECS data needed for subsequent questions. Use pandas to read data directly from the URLs you documented in the warmup when local versions of the files are not available. After download and/or cleaning, write local copies of the datasets. Structure your code to use `exists` from the (built-in) `os` module so the data are only downloaded when not already available locally.

### part a)

Separately for 2009 and 2015, construct datasets containing just the minimal necessary variables identified in the warmup, excluding the replicate weights. Choose an appropriate format for each of the remaining columns, particularly by creating categorical types where appropriate.

### part b)

Separately for 2009 and 2015, construct datasets containing just the unique case ids and the replicate weights (_not_ the primary final weight) in a “long” format with one weight and residence per row.

Question 2 - Construct and report the estimates \[45 points\]
-------------------------------------------------------------

### part a)

Estimate the average number of heating and cooling degree days for residences in each Census region for both 2009 and 2015. You should construct both point estimates (using the weights) and 95% confidence intervals (using standard errors estimated with the replicate weights). Report your results in a nicely formatted table.

For this question, you should use pandas DataFrame methods wherever possible. Do _not_ use a module specifically supporting survey weighting.

### part b)

Using the estimates and standard errors from part a, estimate the change in heating and cooling degree days (base temperature °F) between 2009 and 2015 for each Census region. In constructing interval estimates, use the facts that the estimators for each year are independent and that,

\\\[ \\mathrm{var}\\left(\\hat{\\theta}\_0, \\hat{\\theta}\_1\\right) = \\mathrm{var}\\left(\\hat{\\theta}\_0\\right) + \\mathrm{var}\\left(\\hat{\\theta}\_1\\right), \\\]

when the estimators \\(\\hat{\\theta}\_0\\) and \\(\\hat{\\theta}\_1\\) are independent.

Once again, report your results in a nicely formatted table.

Question 3 - \[20 points\]
--------------------------

Use pandas and/or matplotlib to create visualizations for the results reported as tables in parts a and b of question 2. As with the tables, your figures should be “polished” and professional in appearance, with well-chosen axis and tick labels, English rather than `code_speak`, etc. Use an adjacent markdown cell to write a caption for each figure.

