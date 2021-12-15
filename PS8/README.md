

[Statistics 507, Fall 2021](../index.html)
==========================================

#### Problem Set 8

#### Due Friday December 10 by 5pm

Instructions
------------

Complete all questions of the assignment below and submit to Canvas by the due date. Remember, if you are using late days you should submit a draft of the assignment by the due date and leave a comment indicating how many late days you want to use. **You may not use late days to extend this assignment past 3:30pm on Monday December 13.**

For this problem set, you should submit source code as plain text _shell_ and _python_ script, and a jupyter notebook with the output / answers requested for each question. Use [Jupytext](https://jupytext.readthedocs.io/en/latest/install.html) to associate the jupyter notebook with a markdown `.md` source file.

Questions on this problem set may ask you to use concepts or ideas that have not been discussed in class. One of the goals of these assignments is to help you learn to be independent, read documentation, and otherwise make reasonable decisions about how to analyze and present data, code, or other data science material.

You may discuss the problem set and its solution with your peers, but you are required to work independently on the files to be submitted and to submit your own original work. If you use or closely follow patterns or code from sources other than the course notes or texts you should cite the source.

In addition to the content of your submission, you will be graded on the quality of your source code and the professionalism of your notebook file.

Maintain a consistent and literate style in your scripts and work to make your notebook look professional and well polished. Follow all style rules from previous problem sets.

Question 0 - Slurm \[20 points\]
--------------------------------

In this question you will write a Slurm script and use Great Lakes to compute the cross-validated MSE for one of your Random Forest or Gradient Boosted Tree models from problem set 7.

Using the superconductivity data and either your best performing Random Forest or model or your best performing Gradient Boosted Tree model from problem set 7, write a Python script to compute the 10-fold cross validation error for your chosen model in parallel using 5 sub-processes. The Python script should be written to run in batch mode.

If you didn’t previously divide data into test, validation, and 10 training folds based on unique materials (see `unique_m.csv`), redo the data splitting so that _materials_ (rather than _rows_) are randomized among training folds and the validation and test sets.

Write an associated Slurm shell script to run your multiple process job using 5-6 cores and run the job using the course allocation. Include this Slurm script in your submission.

After running the job using Slurm, use the following command to report usage information: `sacct --format="JobID,NCPUS,Elapsed,CPUTime,TotalCPU"`. Include the output in your notebook.

Here is an example of the output from the `run-mp_isolet.sh` demo:

    $ sacct --format="JobID,NCPUS,Elapsed,CPUTime,TotalCPU,SystemCPU"
           JobID      NCPUS    Elapsed    CPUTime   TotalCPU 
    ------------ ---------- ---------- ---------- ---------- 
    29287742              4   00:00:25   00:01:40  00:52.121 

Question 1 - Tensorflow and Keras \[50 points\]
-----------------------------------------------

In this question you will use Tensorflow and Keras to train deep neural network models using the 80% training sample from question 0. You will then compare these models using the 10% validation sample.

Use the same data partition as for question 0. As stated above, if you didn’t previously divide data into test, validation, and 10 training folds based on unique materials (see `unique_m.csv`), redo the data splitting so that _materials_ (rather than _rows_) are randomized among training folds and the validation and test sets.

### part a \[40 points\]

Train a series of deep neural network regression models to predict the critical temperature from the superconductivity dataset. Train a minimum of 5 models meeting the following conditions:

1.  at least one model has 3 hidden layers,
2.  at least one model has 1-2 hidden layers,
3.  at least one model uses \\(L\_1\\) or \\(L\_2\\) regularization,
4.  at least one model uses dropout,
5.  all models should use MSE or its equivalent as the loss function.

All other details about model architecture are up to you. You may consider more than 5 models, but 5 is the minimum requirement.

Compare your models using the 10% validation set and select the best performing model.

### part b \[10 points\]

Compute and report the MSE on the test dataset for the best performing model from part a.

Question 2 - PySpark and hdfs \[30 points\]
-------------------------------------------

In this question you will use PySpark on the Cavium-ThunderX cluster to compute descriptive statistics from a collection of data files.

The following files should be readable to you in the Cavium hdfs file system at `/user/jbhender/stats507/`:

1.  `user_key.csv` - is a two-column table with columns `user` containing student unique names and `key` containing associated keys used for identifying ownership in the other tables. A user may be associated with more than 1 key.
    
2.  `triangles.csv` - is a 4-column table with columns `triangle_id`, `key`, `base`, and `height`. The `key` column can be used to join against `user_key.csv` to identify users; `base` and `height` can be used to compute area.
    
3.  `rectangles.csv` - is a 4-column table with columns `rectangle_id`, `key`, `length`, and `width`. The `key` column can be used to join against `user_key.csv` to identify users; `length` and `width` can be used to compute area.
    

Check access permissions to these files using the following from your Cavium home directory:

    hdfs dfs -ls /user/jbhender/stats507/

Use these files to compute the following quantities related to the shapes assigned to you:

1.  the total numbers of triangles and (separately) rectangles assigned to you,
2.  the total area of the triangles and (separately) rectangles assigned to you,
3.  the mean areas of your triangles and rectangles.

Submit a Python script that computes these quantities using PySpark and saves them to a csv file, `ps8_q2_<email>_results.csv` replacing `<email>` with your UM unique name. Use this file to create a table or results in your notebook.

You may use either SQL or DataFrame methods for the computations.

