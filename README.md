Optimizing an ML Pipeline in Azure for prediction of Fixed Deposit

##Overview

This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

Summary

This dataset contains data about bank marketing. With the focus on data of the number of times a client was contacted for the campaign, the history of contact, job, loan and housing we seek to predict whether the client opted for a bank deposit or not.
The best performing model was a VotingEnsemble obtained through AutoML with the primary metric accuracy as '0.916570'. 

Scikit-learn Pipeline
In this scikit-learn pipeline a workspace and a curated environment were initialized followed by creating a compute cluster and configuring the training run by creating a HyperDriveConfig and AutoMLConfig for comparison. Finally the run was submitted and the best model was saved and registered. The dataset is tabular which is imported from a URL in the training script. The data is one hot encoded and split into train and test sets. Further the hyperparameters such as C variable (inverse regularization parameter) and maximum number of iterations are set. Accuracy is chosen as the primary metric and logistic regression is the algorithm applied to obtain the best run. Logistic Regression is a Machine Learning classification algorithm that is used to predict the probability of a categorical dependent variable. In logistic regression, the dependent variable (y) is a binary variable.

For parameter sampling, random sampler was used which supports discrete and continuous hyperparameters as well as early termination of low-performance runs. It is also helpful in improving results by doing initial search.

Bandit policy was chosen as the early termination policy. It is based on slack factor/slack amount and evaluation interval. Bandit terminates runs where the primary metric is not within the specified slack factor/slack amount compared to the best performing run.

AutoML
Overall, 23 iterations were performed in 30 minutes duration to obtain the best model. VotingEnsemble is the model generated by AutoML as the best one with the highest accuracy of '0.916570'. The duration it took for this model to run was 1 minute and 26 seconds.
The output showcases a detailed account of all the metrics for the best model.

Pipeline comparison
The best model generated by hyperdrive run had the accuracy of '0.910369'. Whereas, the best model generated by AutoML run had the accuracy of '0.916570'. Therefore, the best overall model was concluded to be the VotingEnsemble generated by AutoML. The main difference between the architecture of hyperdrive run and AutoML run was found to be the specification of parameter sampler and early termination policy in case of hyperdrive run. The reason behind this is that in case of AutoML, these hyperparameters are auto-specified to get the optimum results. This also makes AutoML more time efficient and in this case a better option for obtaining the best model.

Future work
The hyperdrive run took much longer to get the best run because of large number of specified iterations. A viable solution could be the use of a better vm_size and vm_priority as medium and not low if not high. This should help in saving more time if the expense is not significant. 

