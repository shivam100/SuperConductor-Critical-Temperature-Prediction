Introduction
 
Superconducting materials - materials that conduct current with zero resistance - have significant practical applications. Perhaps the best-known application is in the Magnetic Resonance Imaging (MRI) systems widely employed by health care professionals for detailed internal body imaging. Other prominent applications include the superconducting coils used to maintain high magnetic fields in the Large Hadron Collider at CERN, where the existence of Higgs Boson was recently confirmed, and the extremely sensitive magnetic field measuring devices called SQUIDs (Superconducting Quantum Interference Devices). Furthermore, superconductors could revolutionize the energy industry as frictionless (zero resistance) superconducting wires and electrical system may transport and deliver electricity with no energy loss.

In this project we have a statistical model for predicting the superconducting critical temperature on the bases of the features extracted from the superconductor’s chemical formula. The model gives reasonable out-of-sample predictions: ±15 K based on mean-squared error. 

The features are extracted on the bases of thermal conductivity, atomic radius, valence, electron affinity, and atomic mass contribute the most to the model’s predictive accuracy. This is crucial part of the model that it does not predict whether a material is a superconductor or not; but it can only give predictions for superconductors.



























	
Data Description
 
The superconductivity data set contains 21263 rows and 82 columns, which included 81 features variable and 1 target variable “Critical temperature”. The goal of this project is to predict the critical temperature of the superconductor by using their relevant features.  
 
Among all the 81 features variable, that are some variables that are foundation of this data set and used to creating the features to predict the critical temperature, which shown on the table below, and rest of the variables are calculation of Mean, Weighted mean, Geometric mean, weighted geometric mean, Entropy, Weighted entropy, Range, Weighted range, Standard deviation, Weighted standard deviation respectively. 
 
  
  
   
 







Data Exploration and Cleaning
 
Data cleaning and exploration involves dealing with raw data and converting it into a form which is easy to access and analyze.  
 
 Initially we first load the dataset and then obtain the first five rows in order to get an overview of what the columns are and their respective datatypes. 
 
 
We then find the information to display the number of columns, column labels, column data types, memory usage, range index, and the number of cells in each column (non-null values) 
  
 
 
 
  
 
 
 



 



























Data Exploration and Visualization
 
Exploring data and displaying it in a visual form is an important tool to help tell us a story, making it easy to understand by highlighting trends and outliers. Removing excess noise, gives us a clear picture and helps enable us to draw coherent conclusions about the data. 
 
 
To understand the unique features in the model we get the results column wise to understand the nature of the model. 
 
  
 
 
We obtain the details of the dataset and we can see that there are extreme values between in the Atomic Mass column : 6 and 21263.  
 Page Break 
 
Since we aim to clean the data so that it becomes much easier to analyze we need to make sure that there are no null values as that would cause poor reporting and skewed analysis.  
 
We could check the missing in the dataset by the following method and it shows that there are no null values in this dataset. In this case since it is a 0 or 1 i.e., hence we do not need to make any data changes to this dataset. 
 










































Dimension reduction
 
Before we apply any learning algorithms to our dataset, we are going to perform the principal component analysis to reduce the computational complexity to our dataset, especially for the random forest tree and decision tree we will implement later which involved a lot of computation. 
 
We first standardized the dataset, performed the algorithm, found the dimensions with the greatest variation to maximize the distinction between different data points. We calculated the cumulative explained variance and visualized it by the line chart in order to get a better sense of how many components to choose from. 
  
 
What we see from the chart above is that the first few components captured a great amount of variation, and gradually decreased. The goal is to reduce the dimensions and not lose too much variance. Thinking of tradeoff between these two aspects, we decided to keep principal component as 15 which captured 94% of the cumulative explained variance. 

Now After PCA was performed and we had identified our important 15 features, we decided to perform different kinds of regressions and compare the result.











 
Linear Regression
 
The first method we are going to implement is linear regression, one of the most used algorithms and we serve it as the baseline model to compare the performance with other methods we choose. We apply all possible techniques that we covered from class and set the learning with 0.00001, and tolerance with 0.00005 for gradient descent, L1 & L2 regularization, also the normal equation as well to check if there is any improvement. 
 
 
Gradient descent: 
  
 
Gradient descent with L1 Regularization: 
  
 
Gradient descent with L2 Regularization: 
  
 
Normal Equation: 
  
 
All the results are very similar to each other, but Normal equation perform the best, with lowest MSE 477.6916 and RMSE 21.8561 respectively. 
 
 









Decision Trees
As we saw above that the Linear Regression does a fairly nice job in minimizing the MSE of the predicted results, we still wanted to experiment with methods like Decision trees and Random Forest regression methods to see if there are any further improvements in the prediction.
 Decision tree builds regression or classification models in the form of a tree structure. It breaks down a dataset into smaller and smaller subsets while at the same time an associated decision tree is incrementally developed. The final result is a tree with decision nodes and leaf nodes. 
 
In general, decision tree is a more flexible method compared to Linear Regression and it should be able to reduce the bias considerably by making improved predictions. Below are the error stats calculated after performing the Decision trees regression. The parameter values were: max_depth – 10, min_samples_split – 1000.
MSE   342.4764 & RMSE  1850612
It is a slight improvement over the Linear Regression model.
Max_depth – Maximum number of depth or branch nodes the root node can have
Min_samples_split – Split function will be applied if the node size(no of observations) is greater than or equal to this value
When we used decision trees to print the tree, it was as follows:
 








Random Forest Regression
After Observing the much better results using Decision Tree Regression, we decided to try Random Forest Regression is a supervised learning algorithm that uses ensemble learning method for regression. Ensemble learning method is a technique that combines predictions from multiple machine learning algorithms to make a more accurate prediction than a single model.the more complicated, yet better ensemble approach knows as Random Forest Regression. 

 
Here we set the number of trees as 2 and the seed value to 42 to perform then ran the Model. 

The random Forest Regression after training was used to predict against the test model and it was able to do so successfully with a MSE of 177.23. 






K-means clustering
Though the main problem here is to predict a response variable, we were just curious to see if there are any clusters found in the data, and wanted to study the K-means algorithm by coding it from scratch. Using the elbow method, we plotted the below chart to find the optimal k-value for the clusters.
 
From the above chart, we can see that an elbow is created at the k-value 2. Hence we have chosen k-value as for creating the clusters.
Then the k-value is fed to the clustering algorithm to produce the clusters by minimizing the within cluster variation(distance) and maximizing the inter-cluster distances for each observation. After clustering the data points, the below chart is created in-order to visualize the clusters.
 
[Note: In order to visualize the clusters, we applied PCA to reduce the dimensions to 2 from 81].

Conclusion
In conclusion, we had a dataset which had 82 features which we thought were used in determining the critical temperature of the superconductor. After the initial data exploration and going through the corelations, we realised that not all features are used and hence we can use the Dimension Reduction Methods to decrease the number of features used to prediction. 
After applying the PCA Technique, we came up with 15 features which were having more impact in determining the actual temperature. Now we started with various regression models to perform a comparative analysis which one will be working best. 
After training the algorithms, we tested them against the test data which we had split out from the original data. 
The average value for MSE for all Linear Regression Models was 477.758
The average value of MSE for Decision Tree Regression Model was 342.47
The average value for MSE for Random Forest Regression Model was 177.23

Which gives enough evidence that the ensemble Random Forest Regression Model was able to determine the temperature with least error. 















References:
•	Random Forest Regression link 
•	A data-driven statistical model for predicting the critical temperature of a superconductor link
