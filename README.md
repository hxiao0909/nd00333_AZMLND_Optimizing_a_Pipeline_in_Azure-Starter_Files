# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
This dataset contains data about customer information for bank marketing purposes. We are seeking to predict if a customer is subscribed to a fixed term deposit, which is a binary classification problem.

According to AutoML, the best performing model was a **VotingEnsemble** model.

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

Load data -> Train/test split -> configure searching space and early termination policy -> start hyperparameter. tuning -> choose the best model by looking at the metrics

**What are the benefits of the parameter sampler you chose?**

Since we are using a Logistic regression, the only two parameters we are tuning is the regularization strength C and max number of iteration. I used a uniform distribution between [0, 1] for C values, and a discrete sample of [100, 150, 200, 250] for max_iter. We have no prior knowledge how the C values distribute, so a uniform distribution will give equal chance for all values.

**What are the benefits of the early stopping policy you chose?**

I used the Bandit policy, which will terminate the run when the primary metric is not within the specified slack factor/slack amount compared to the best performing run. For a simple classification problem like this one, since the searching space is not very complicated and we are less likely to be trapped in a local minimum, the Bandit poilicy would terminate quick enough and keeps a good result.

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

AutoML went through a lot of different models and the best one I got was a VotingEnsemble model.

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

The AutoML best model had a slighly higher accuracy 0.9173, but the Logistics Regression did no worse than that, probably because the problem is quite simple. With more complicated problems, I think I would prefer using AutoML first to find several good model candidates, and then tune the hyperparameters again to see if they get even better. If I have customized algorithms, of course the hyperparameter tuning would be my choice.

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

There's data imbalance in this dataset and I hadn't had time to take care of it. Fixing that problem will very likely improve the  And also I would love to try some other configurations with both methods. 

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**

**Image of cluster marked for deletion**

I deleted the cluster in from the portal/console, instead of the notebook, and nothing is left in the cluster tab now. So I cannot get the screen shot.
