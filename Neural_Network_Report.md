# Neural Network Report

## Overview

In order to best allocate grant funding to companies most likely to be successful when financially assisted, we have developed a Neural Network Machine Learning model to analyze our past funding disbursements, and come up with a prediction model on future potential applicant's chances of success if we provide funding. This will be especially useful for the organization, as it allows us to most effectively utilize our own funds, and minimize the chances of funding going to companies more likely to miss the mark. We want to minimize this as much as possible in order to prevent the opportunity cost to other companies who might have a better chance to succeed had they been given the funds instead.

## Results

# Data Preprocessing

Reviewing the aggregate data revealed some potential problems for our model, including unnecessary information, potential data outliers, and the existence of non-numeric data. In order to prepare the data for the model, we took the following steps:

* Removed the "Name" and "EIN" identification columns as they would not be a factor for analysis.

* Reduced the number of output results for both "Classification" and "Application_Type" data in order to reduce the effect of outliers on the model.

* Converted non-numeric, categorical data into numeric classifications the model would be able to take into account as part of the component analysis.

* Utilized a scaling method on the data in order to reduce large variability within numbers, helping the model to be more accurate in its analysis and prevent over-weighting of certain components.

* Determined the "Application_Type", "Affiliation", "Classification", "Use_Case", "Organization", "Status", "Income_Amt", "Sepcial_Considerations", and "Ask_Amt" columns to be the features for the model, while the target for the model was the "Is_Successful" data. We felt the feature data selected all made sense to consider when looking at whether or not the funded entity was successful or not, hence the choice in picking the "Is_Successful" data as the target.

# Compilation, Training, and Evaluation

Throughout the process of building the model, we found it necessary to attempt some optimizations in order to increase performance. The initial model contained two hidden layers with an output layer, with 80 units in the first and 30 units in the second. We also utilized the Relu activation algorithm for training over a period of 100 epochs. Performance (outlined below) was not quite to the desired level, so several optimization attempts were made to try and improve performance:

* Initial Model
    - 2 hidden layers (80/30units, relu activation)
    - 100 epochs
    - Training Loss/Accuracy: 0.5342/0.7403
    - Testing Loss/Accuracy: 0.5665/0.7291

* Optimization Attempt One
    - **3 hidden layers** (80units/30/12units, relu activation)
    - 100 epochs
    - Training Loss/Accuracy: 0.5399/0.7373
    - Testing Loss/Accuracy: 0.5610/0.7287

* Optimization Attempt Two
    - 3 hidden layers **(80/60/40units, tanh activation)**
    - 100 epochs
    - Training Loss/Accuracy: 0.5364/0.7393
    - Testing Loss/Accuracy: 0.5661/0.7264

* Optimization Attempt Three
    - **4 hidden layers (30/30/20/12units, relu activation)**
    - **500 epochs**
    - Training Loss/Accuracy: 0.5288/0.7422
    - Testing Loss/Accuracy: 0.6283/0.7266

## Summary

In an interesting turn of events, the model with the original parameters seemed to perform best out of all attempts made. The initial model provided the best accuracy by a small amount, with only a slight increase in loss of data. Additionally, the spread between the training and testing results were in-line with each other. This was surprising, as the other models boasted additional hidden layers, which we had hoped would allow the model to better fit the testing data. It was also noticeable that the loss of testing data went up considerably when adding a larger number of epochs in the third optimization attempt, even with the number of neurons in each hidden layer reduced. While we thought this might provide the model more time to work out a stronger solution, it appears as though these last optimization attempts were more likely to begin overfitting the training data.

As it stands, there appears to be a roughly 70% chance of the model correctly predicting the outcomes, but the loss rate comes in at over 50% indicating that the predicted values the model determines are about as accurate to the testing data as a little worse than a coin flip. Due to this high level of variability in the overall performance against the testing data, it is difficult to strongly recommend this model for future use, even with the decent level of accuracy achieved. If further optimization tests were carried out, we would recommend adjusting parameters in the pursuit of an accuracy above 75% (ideally above 80%), while bringing the loss rate to .40 or below, if possible.

As another option, it may prove useful to utilize a random forest model and compare the results to the neural network. Random forests have proven capable with similar problems, and may be a better way to approach this particular question. If the random forest model is less accurate than current results with the neural network, we would recommend continuing layer and neuron adjustments, as well as considering a much larger number of epochs for the model to train with.
