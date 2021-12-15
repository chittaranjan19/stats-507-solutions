
[Statistics 507, Fall 2021](../index.html)
==========================================

#### Problem Set 4

#### Due Friday October 22 by 5pm.

Instructions
------------

Complete all questions of the assignment below and submit to Canvas by the due date. Remember, if you are using late days you should submit a draft of the assignment by the due date and leave a comment indicating how many late days you want to use.

For this problem set, you should submit source code as plain text Python scripts (with extension `.py`) and an associated Jupyter notebook (with extension `.ipynb`). Use [Jupytext](https://jupytext.readthedocs.io/en/latest/install.html) and (preferably) the _light_ format to associate the two files.

Questions on this and future problem sets may ask you to use concepts or ideas that have not been discussed in class. One of the goals of these assignments is to help you learn to be independent, read documentation, and otherwise make reasonable decisions about how to analyze and present data, code, or other data science material.

You may discuss the problem set and its solution with your peers, but you are required to work independently on the files to be submitted and to submit your own original work. If you use or closely follow patterns or code from sources other than the course notes or texts you should cite the source.

In addition to the content of your submission, you will be graded on the quality of your source code and the professionalism of your notebook file.

Maintain a consistent and literate style in your Python script and work to make your notebook look professional and well polished. Follow all style rules from previous problem sets.

When asked for a nicely formatted table you should produce one using HTML (perhaps via Markdown) and it should follow standards suitable for publication, e.g. columns should be named in English rather than `code_speak`. _Tables should also be produced using code_ so that minimal manual work would be needed to update the tables if the results were to change.

Question 0 - Topics in Pandas \[25 points\]
-------------------------------------------

For this question, please pick a topic - such as a function, class, method, [recipe or idiom](https://pandas.pydata.org/pandas-docs/stable/user_guide/cookbook.html) related to the pandas python library and create a short tutorial or overview of that topic. The only rules are below.

1.  Pick a topic _not_ covered in the class slides.
2.  Do not knowingly pick the same topic as someone else.
3.  Use bullet points and titles (level 2 headers) to create the equivalent of **3-5** “slides” of key points. They shouldn’t actually be slides, but please structure your key points in a manner similar to the class slides (viewed as a notebook).
4.  Include executable example code in code cells to illustrate your topic.

You do _not_ need to clear your topic with me. If you want feedback on your topic choice, please discuss with me or a GSI in office hours.

Question 1 - NHANES Table 1 \[35 points\]
-----------------------------------------

As discussed previously in class, academic papers reporting on human subjects typically include a “table 1” summarizing the demographics of the subjects included. This table is typically stratified into columns by a key exposure, outcome, or other important variable.

When there are subjects with missing outcomes, it is common to include a table like described above examining the (marginal) relationships between missingness and key demographics. This helps an interested reader reason about possible selection bias stemming from those for whom the outcome is observed being different in some ways from those for whom it is not.

In this activity, we will construct a balance table comparing demographics for those who are or are not missing the oral health examination in the NHANES data prepared in [Problem Set 2](https://jbhender.github.io/Stats507/F21/ps/ps2.html), Question 3.

### part a)

Revise your solution to PS2 Question 3 to also include gender (RIAGENDR) in the demographic data.

_Update (October 14)_: Include your data files in your submission and with extension `.pickle`, `.feather` or `.parquet` and include a code cell here that imports those files from the local directory (the same folder as your .ipynb or .py source files).

### part b)

The variable `OHDDESTS` contains the status of the oral health exam. Merge this variable into the demographics data.

Use the revised demographic data from part a and the oral health data from PS2 to create a clean dataset with the following variables:

*   id (from SEQN)
*   gender
*   age
*   under\_20 if age < 20
*   college - with two levels:
    *   ‘some college/college graduate’ or
    *   ‘No college/<20’ where the latter category includes everyone under 20 years of age.
*   exam\_status (RIDSTATR)
*   ohx\_status - (OHDDESTS)

Create a categorical variable in the data frame above named ohx with two levels “complete” for those with `exam_status == 2` and `ohx_status == 1` or “missing” when `ohx_status` is missing or corresponds to “partial/incomplete.”

### part c)

Remove rows from individuals with `exam_status != 2` as this form of missingness is already accounted for in the survey weights. Report the number of subjects removed and the number remaining.

### part d)

Construct a table with `ohx` (complete / missing) in columns and each of the following variables summarized in rows:

*   age
*   under\_20
*   gender
*   college

For the rows corresponding to categorical variable in your table, each cell should provide a count (n) and a percent (of the row) as a nicely formatted string. For the continous variable age, report the mean and standard deviation \[Mean (SD)\] for each cell.

Include a column ‘p-value’ giving a p-value testing for a mean difference in age or an association beween each categorical varaible and missingness. Use a chi-squared test comparing the 2 x 2 tables for each categorical characteristic and OHX exam status and a t-test for the difference in age.

\*\*Hint\*: Use `scipy.stats` for the tests.

Question 2 - Monte Carlo Comparison \[40 points\]
-------------------------------------------------

In this question you will use your functions from problem set 1, question 3 for construcing binomial confidence intervals for a population proprotion in a Monte Carlo study comparing the performance of the programmed methods.

In the instructions that follow, let \\(n\\) refer to sample size and \\(p\\) to the population proportion to be estimated.

Choose a nominal confidence level of 80, 90 or 95% to use for all parts below.

You may wish to collect your confidence interval functions in a separate file and import them for this assignment. See [here](https://stackoverflow.com/questions/20309456/call-a-function-from-another-file) for helpful discussion.

_Update, October 14_ - Make sure to correct any mistakes in your functions from PS1, Q3. It is also acceptable to revise your functions to use vectorized operations to make the Monte Carlo study more efficient.

### part a) Level Calibration

In this part, you will examine whether the nominal confidence level is achieved by each method over a grid of values for \\(n\\) and \\(p\\). Recall that the _confidence level_ is the proportion of intervals that (nominally should) contain the true population proportion.

Pick a sequence of values to examine for \\(p \\in (0, 0.5\]\\) or \\(p \\in \[0.5, 1)\\) and a sequence of values for \\(n > 0\\). For each combination of \\(n\\) and \\(p\\) use Monte Carlo simulation to estimate the actual confidence level each method for generating intervals achieves. Choose the number of Monte Carlo replications so that, if the nominal level were achieved, the margin of error around your Monte Carlo estimate of the confidence level would be no larger than 0.005.

For each confidence interval method, construct a [contour plot](https://matplotlib.org/stable/gallery/images_contours_and_fields/contour_demo.html) (with axes n and p) showing the estimated confidence level. Use subplots to collect these into a single figure.

### part b) Relative Efficiency

As part of your simulation for part a, record the widths of the associated confidence intervals. Estimate the average width of intervals produced by each method at each level of \\(n\\) and \\(p\\) and use a collection of contour plots to visualize the results. Finally, using the Clopper-Pearson method as a reference, estimate the average _relative_ width (at each value of \\(n\\) and \\(p\\)) and display these results using one more countour plots.

