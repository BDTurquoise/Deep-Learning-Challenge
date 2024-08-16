# Module 21 Report - Deep Learning Challenge

## Overview of the Analysis

- The purpose of this analysis is to use available metadata to create a binary classifier to predict whether applicants funded by the non-profit group Alphabet Soup will be successful or not.

- The metadata being utilized includes EIN, Name, Application Type, Affiliation, Classification, Use Case, Organization Type, Active Status, Income Amount, Special Considerations, and ask amount. These values help us to predict whether funding provided by Alphabet Soup will be used effectively or not.

## Stages of the Deep Learning Model Process

1.  Data Preprocessing:

    - The variable we are targeting for the model in this instance is the 'IS_SUCCESSFUL' variable.

    - The features for this model are the following: Name, Application Type, Affiliation, Classification, Use Case, Organization Type, Income Amount, and Ask Amount.

    - The non-beneficial variables that are being remove are: EIN, Status, and Special Considerations.

    - To assist with feature selection, the results of an feature importance analysis using a Random Forest model were examined. The most important features identified were the Ask Amount and the Affiliation, while the least important features were the Status and Special Considerations.

2.  Compiling, Training, and Evaluating the Model:

    - For my initial model, I used three different layers, ecxcluding the input layer. The two hidden layers had 80 and 30 neurons, respectively, and both used ReLU as the activation function. The output layer had 1 neuron and utilized a Sigmoid activation function. This design was used as it is typical for a binary classification neural network.

    - With the initial model, I was unable to achieve the target performance. I then sought to optimize the model using the follwing steps:

           Optimization attempt 1: Failed (72.65% / Loss: 0.5665)

           -Added a hidden layer and increased the number of neurons in order to improve the model capacity and ability to learn   interactions between the input features

           -Added dropout to attempt to prevent overfitting and improve generalization

           -Added a learning rate to control the step size

          Optimization attempt 2: Failed (72.55% / Loss: 0.5959)

          -Re-included the name ID colum at the recommendation of a colleague and set cateogrical threshold at 500 and dropped the status and special considerations columns

          -Split ask amount into categories of 5000 and others on a recommendation of a colleague to try to simplify the feature

          -Changed loss type to huber at the recommendation of a colleague; this was because huber is more likely to be robust to outliers and takes a balanced approach to penalizing errors. This did drop the loss to 0.0937.

          -Increased number of layers and neurons

          Optimization attempt 3: Failed (72.37% / Loss: 0.0943)

          -Re-dropped the name column as no benefit to the model was noticed

          -Kept the ask amount category split of 5000 and others

          -Changed activation type to swish as it has been found to outperform relu in some instances

          -Tested using optimizer AdamW combined with a learning rate of 0.0001

## Summary:

- In summary, the overall results of the deep learning model constructed were not able to be elevated above 72%. In terms of predictive capability, this leaves much to be desired. However, this could potentially be improved by using a different model. In researching the different types of models, I believe that using an XGBoost model would yield better results.

- Reasons for inferring XGBoost model would improve results:

  -The Categorical Features like APPLICATION_TYPE and CLASSIFICATION typically have non-linear relationships with the target because each category might have a different impact that isn’t directly proportional.

  -Numeric Features like ASK_AMT might exhibit either linear or non-linear relationships. Often, large ranges or skewed distributions can lead to non-linear effects.

  -XGBoost is purported to perform better when dealing with complex non-linear relationships. XGBoost also includes regularization parameters which help prevent overfitting. Due to these strengths and the fact we can expect both linear and non-linear relationships from our features, XGBoost might very well be a good choice.
