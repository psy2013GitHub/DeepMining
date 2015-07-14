## Deep Mining : Copula-based Hyperparameter Optimization for Machine Learning Pipelines ##

This repositery contains all the code implmenting the Gaussian Copula Process (GCP) and a hyperparameter optimization technique based on it.
All the code is in Python and mainly uses Numpy, Scipy and Scikit-learn.
The GCP code is based on Scikit-learn's GP implementation.

### Python scripts ###
- gcp.py .....................................................................The class implementing the GCP
- GCP_utils.py .........................................................................Utility functions for GCP
- smart_sampling.py ..........................................Script to run the optimization process
- sampling_utils.py .....................................Utility function for the optimization process
- sklearn_utils.py ..........................................................Utility function from Scikit-learn
- run_experiment.py .................................Script to run several trials on a test instance
- Test/analyze_results.py ..............The code to compute the Q scores based on a trial
- Test/run_result_analysis.py ............................Run analyze_results script and save it

### Instructions ###
One can easily run a GCP-based hyperparameter optimization process thanks to this code.
To run it on a new pipeline, create a folder *newPipeline* in the Test folder, and create a Python script as run_exp.py in SmartSampling_CodeTest.
The SmartSmapling function has many parameters but most of them have default values.
Basically the user jsut has to provide a *scoring_function* and a *parameter_bounds* array (n_parameters,2). The software will try to find the best parameter set within these ranges by iteratively calling the *scoring_function*.

### Examples ###
This repository contains two tests GCP_CodeTest and SmartSampling_CodeTest that enable the user to quicly test the GCP and SmartSampling code.

It also contains two real examples based on the Sentiment Analysis problem for IMDB review (cf. [Kaggle's competition](https://www.kaggle.com/c/word2vec-nlp-tutorial)) and the Handwritten digits one from the MNIST database (cf. [Kaggle's competition](https://www.kaggle.com/c/digit-recognizer)).
In order to quickly test the optimization process, a lot of off-line computations have already been done and stored in the folders *Test/ProblemName/scoring_function*. This way, the scrip run_experiments makes it easy to run fast experiments by querying those files, instead of really building the pipeline for each parameter test.

Directory structure :
Each test instance follows the same directory structure, and all files are in the folder Test/ProblemName.
- run_test.py : run several trials by setting the configuration for the script run_experiment
- scoring_function/ : the off-line computations stored. params.csv contains the parameters tested, and output.csv the raw outputs given by the scoring function (all the cross-validation estimation). The files *true_score_t_TTT_a_AAA* refer to the Q scores computed with a threshold == TTT and alpha == AAA
- exp_restuls/expXXX : run_test stores the results in the folder expXXX where XXX is a integer refering to a configuration
- exp_results/transformed_t_TTT_a_AAA/expXXX : the analyzed results from the trial expXXX, computed by run_result_analysis with a threshold == TTT and alpha == AAA. 
