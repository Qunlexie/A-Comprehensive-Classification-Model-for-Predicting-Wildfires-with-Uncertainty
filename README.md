# A-Comprehensive-Classification-Model-for-Predicting-Wildfires-with-Uncertainty
## Abstract
Using a comprehensive dataset consisting 1713 samples: 1327 instances of the class “no_fire” and 386 instances of the “fire” class, I used 11 classification models to predict whether or not there is an occurrence of wildfire using the three feature variables: Normalized Difference Vegetation Index (NDVI), Land Surface Temperature (LST) and the Thermal Anomalies (referred to as the BURNED_AREA in the dataset). The aim of this work is to compare the performance of different Machine learning models (with careful hyperparameter selection) for wildfire prediction. The results were obatained for two cases: with balanced class weight and without class weight balance. 


## Introduction 
I came across this paper by Younes Oulad Sayad, Hajar Mousannif, Hassan Al Moatassime (2019) titled Predictive modeling of wildfires: A new dataset and machine learning approach. Wildfires are a serious environmental problem today, heightened by the menace of global warming and climate change. This work introduced a new data set for predicting the occurrence of wildfires using processed remote sensing data. Some brief on their work is given below:
“This Dataset was created based on Remote Sensing data to predict the occurrence of wildfires, it contains Data related to the state of crops (NDVI: Normalized Difference Vegetation Index), meteorological conditions (LST: Land Surface Temperature) as well as the fire indicator “Thermal Anomalies”. All three parameters were collected from MODIS (Moderate Resolution Imaging Spectroradiometer), an instrument carried on board the Terra platform. The collected data went through several preprocessing techniques before building the final Dataset. The experimental Dataset is considered as a case study to illustrate what can be done at larger scales” (Oulad Sayad et al, 2019)

In their work they used 804 data samples out of the 1713 samples available to predict the occurrence of wildfires using two Machine Learning models: Neural Network and Support Vector Machines (SVM). Here, I use the full dataset consisting 1713 samples: 1327 instances of the class “no_fire” and 386 instances of the “fire” class (More details on this data can be found here). Also, I used 11 classification models to predict whether or not there is an occurrence of wildfire using the three feature variables: Normalized Difference Vegetation Index (NDVI), Land Surface Temperature (LST) and the Thermal Anomalies (referred to as the BURNED_AREA in the dataset). The aim of this work was to compare the performance of different Machine learning models (with careful hyperparameter selection) for wildfire prediction. The full code for this work can be found in my Github: https://github.com/Qunlexie/A-Comprehensive-Classification-Model-for-Predicting-Wildfires-with-Uncertainty.


## Method/ML Models
1. Support Vector Machines: A support Vector Classfier is one that chooses the best hyperplane that maximises distance between the two classes. The non-linear ‘rbf’ kernel tends to perfrom better for this task so it was kept constant in the grid search. However, the C values and the gamma values were varied. The grid search parameters are given below. The best combination was then used in the classification model and the crossvaligdation accuracy (k-fold with k=5) and the standard deviation was recorded. the standard deviation is used to understand the uncertainty of the model.
param_grid = {'C': np.logspace(1, 2.3, 10), 'gamma': np.linspace(0,2, 5), 'kernel': ['rbf']}
2. Bagging Classifier: The idea of the bagging classifier is to be able to combine several simple classifiers to create a more complex classification boundary. Here several SVM classifiers were pooled together or ‘bagged’. This model was tuned using a grid search method over a range of hyperparameters selected. The grid search parameters are given below:
param_grid = {'n_estimators': list(range(0, 110, 10))[1:], 'max_features': list (range(1,21, 2))}
3. Extremely Randomised Trees Classifier: Extremely randomized trees pick a node split very extremely (both a variable index and variable splitting value are chosen randomly as opposed to Random Forest that finds the best split (optimal one by variable index and variable splitting value) among random subset of variables [1]. This model was tuned using a grid search method over a range of hyper parameters selected. The grid search parameters are given below:
param_grid = {'n_estimators': list(range(0, 110, 10))[1:], 'max_features': list (range(1,21, 2)), 'max_depth' :list(range(1,21, 2))}
4. Adaboost Classifier: AdaBoost or Adaptive Boosting classifier builds a strong classifier by combining multiple poorly performing classifiers so that you will get high accuracy strong classifier. The basic concept behind Adaboost is to set the weights of classifiers and training the data sample in each iteration such that it ensures the accurate predictions of unusual observations [2]. The AdaBoost Classification model was tuned using a grid search method over a range of hyper parameters selected. The grid search parameters are given below:
param_grid = {'n_estimators': list(range(0, 110, 10))[1:], 'learning_rate': [0.2, 0.4, 0.6, 0.8, 1]}
5. Gradient Boosting Classifier: Gradient boosting classifiers are the AdaBoosting method combined with weighted minimization, after which the classifiers and weighted inputs are recalculated. The objective of Gradient Boosting classifiers is to minimize the loss, or the difference between the actual class value of the training example and the predicted class value [3]. The Gradient boosting classifier was tuned using a grid search method over a range of hyper parameters selected. The grid search parameters are given below:
param_grid = {'n_estimators': list(range(0, 110, 10))[1:], 'max_features': list (range(1,21, 2)), 'max_depth' :list(range(1,21, 2))}
6. Extreme Gradient Boosting (XGBOOST) Classifier: XGBoost is a refined and customized version of a gradient boosting decision tree system, created with performance and speed in mind. XGBoost actually stands for “eXtreme Gradient Boosting”, and it refers to the fact that the algorithms and methods have been customized to push the limit of what is possible for gradient boosting algorithms [3]. The XGBOOST classifier was tuned using a grid search method over a range of hyper parameters selected. The grid search parameters are the same as those of the Gradient Boosting classifiers
7. Random Forest: It is an ensemble tree-based learning algorithm. The Random Forest Classifier is a set of decision trees from randomly selected subset of training set. It aggregates the votes from different decision trees to decide the final class of the test object [4]. The Random forest classifier was tuned using a grid search method over a range of hyper parameters selected. The grid search parameters are same as those of the Gradient boosting classifiers and Extremely Randomized Trees.
8. Neural Network: Neural networks are built of simple elements called neurons, which take in a real value, multiply it by a weight, and run it through a non-linear activation function. By constructing multiple layers of neurons, each of which receives part of the input variables, and then passes on its results to the next layers, the network can learn very complex functions [5].
param_grid = {'hidden_layer_sizes': list(range(0, 51, 5))[1:]}
9. Nearest Neighbour classifier: Classifies each data point by analyzing its nearest neighbors from the training set. The current data point is assigned the class most commonly found among its neighbors. The algorithm is non-parametric (makes no assumptions on the underlying data) and uses lazy learning (does not pre-train, all training data is used during classification) [5]. In the Nearest Neighbour Classifier, using a grid search method, the size of the hidden layers was the hyperparameter varied. Details on the range defined is given below:
param_grid = {'n_neighbors': list(range(1, 15, 2))}
10. Gaussian Naive Bayes Classifier: A probability-based classifier based on the Bayes algorithm. According to the concept of dependent probability, it calculates the probability that each of the features of a data point (the input variables) exists in each of the target classes. It then selects the category for which the probabilities are maximal [5].
11. Stochastic Gradient descent classifier: Stochastic Gradient Descent is similar to the gradient descent except that it uses a different type of optimiser. The difference being that in SGD, the gradient of the cost function is obtained for a single example at each iteration instead of the sum of the gradient of the cost function of all the examples [6]. In the Stochastic Gradient descent classifier, using a grid search method, the type of loss function was the hyperparameter varied. Details on the range defined is given below:
param_grid = {'loss': ['hinge', 'log', 'modified_huber', 'squared_hinge', 'perceptron', 'squared_loss', 'huber', 'epsilon_insensitive', 'squared_epsilon_insensitive']}

## Discussion 
### Without Class Weight Balance
A class imbalance occurs since data samples in the ‘no_fire’ class is way more than that in the ‘fire’ class. Here the analysis was done without balancing the classes. The effect of class weight balancing can significantly affect the performance of the classifier.
The best accuracy among the 11 models is obtained using the Random Forest classifier. The best Random Forest parameters used to fit the model (as obtained from grid search) is given below: {'max_depth': 16, 'max_features': 1, 'n_estimators': 40}
The accuracy is 84.76%. The standard deviation is used in this analysis to depict the uncertainty in the models. The model uncertainty for the best model is reasonably low with a standard deviation of 2.44%. Four of the classifiers have accuracy values above 80% and they are: Extremely Randomised Trees, Gradient Boosting, Extreme Gradient Boosting and Random Forest classifiers. The lowest accuracy is obtained with the stochastic gradient descent algorithm though it also has the best standard deviation (least uncertainty). The accuracy of the Random Forest classifier and the Gradient boosting classifier is almost the same with the random forest predicting with lower uncertainty compared to the Gradient Boosting classifier. Beyond the best three classifiers, the SVM and the bagged SVMs tend to perform better than their remaining counterparts.

### With Class Weight Balance
Here, the class weights were balanced for 4 of the classification models: Support Vector Machine, bagging Classifiers (of SVMs ), Extra Trees Classifier, Stochastic Gradient Descent. The accuracy tend to drop but the number of correctly classified no_fire class is increased in the classification report i.e. fewer mistakes are made in classifying the no_fire class (more details on the classification reports can be found in the Github code). The bar chart below shows the accuracy values for all classifiers including those with class weight balance.

## Conclusion 
The Random Forest Algorithm tend to perform better than other classifiers for the wildfire prediction problem. Note that the accuracy values obtained in this work is lower than those obtained in the original paper, this is is because more samples of data were used.

## References
[1] Extremely randomized trees: https://docs.opencv.org/2.4/modules/ml/doc/ertrees.html
[2] AdaBoost Classifier: https://www.datacamp.com/community/tutorials/adaboost-classifier-python
[3] Gradient boosting Classifiers: https://stackabuse.com/gradient-boosting-classifiers-in-python-with-scikit-learn/
[4] Random Forest Classification: https://towardsdatascience.com/random-forest-classification-and-its-implementation-d5d840dbead0
[5] Types of Classification Algorithms: Which Is Right for Your Problem?: https://missinglink.ai/guides/neural-network-concepts/classification-neural-networks-neural-network-right-choice/
[6] ML | Stochastic Gradient Descent (SGD): https://www.geeksforgeeks.org/ml-stochastic-gradient-descent-sgd/


More details on the result analysis can be found here: https://sites.tufts.edu/olukunleowolabi/2020/03/15/a-comprehensive-classification-model-for-predicting-wildfires-with-uncertainty/
