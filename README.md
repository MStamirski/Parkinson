# Parkinson

Datasets in this projects come from Kaggle competition "amp-parkinsons-disease-progression-prediction". The goal was to predict 4 ratios ("updrs") which measure Parkinson disease progression. Predictions were based on clinical and neurobiological data of patients, spread over time. Proposed metric in this project was sMAPE, which returns values in range from 0 to 200.

I tried to deal with the problem in two fields. First was feature engineering, second was improvement of results of computed regression. I tested many models, including neural networks (which is not included in this repository), and finally choose LGBMRegressor.

* notebook "project 1"

In first notebook I conducted detailed datasets analysis. It was hindered because of final number of features: 1197. At first nulls were replaced with averages in specific subsets, but finally it turned out, that replacement with zeros gave better results. 

Then I examined different variants of feature selection, based on decreasing correlation with predicted label.

My idea to improve the results was to divide features into subsets, where predictions would be made using separately trained regression models. I implemented it by unsupervised clustering with KMeans model, chosen after many trials (not included in this repository). 

Final set of optimal parameters - i.e. number of features and number of clusters for each label prediction - was found experimentally, by evaluating many changing combinations. It improved initial sMAPE of about 8 points.

* notebook "project 2"

In second notebook I normalized features values. Then I performed a dimensionality reduction, using model LocallyLinearEmbedding. Optimal number of components was determined experimentally. It improved sMAPE before clustering of about 4 points. After applying optimal number of clusters it decreased of another 4 points.

At the end I modified function which divides features to clusters, taking into account, that validation (and testing) data wouldn't participate in clusters calculation. The clusters will be established on the basis of training dataset, and validation data assignment to clusters should be predicted. This assumptions introduced an error of cluster prediction, which, unfortunatelly, removed the positive impact of clustering to final sMAPE.
