# Tanzanian Waterpoint Classification

![Pumping Photo](images/pumping.jpg "Tanzanian Water Pump")
image courtesy of [flickr user christophercjensen](https://www.flickr.com/photos/christophercjensen/3559607145)

## Author: Michael Erb

## Problem

The Tanzanian Ministry of Water needs to ensure that clean, potable water is available to communities across Tanzania using limited resources.

That water can be provided by improving the maintenance of existing waterpoints and by expanding the number of waterpoints

If we can accurately classify a waterpoint, the Ministry will have a better understanding of their existing infrastructure, and because of cost savings, will be able to reallocate existing resources to expand the water infrastructure.

The ministry needs to be able to predict which class the waterpoints belong to: functional, functional but need some repairs, and non-functional.

## Data

Data is provided by [Taarifa](http://taarifa.org/) and the [Tanzanian Ministry of Water](http://maji.go.tz/) originally as part of a competition hosted by [DrivenData](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/).

It contains approximately 60,000 instances.

It is stored in the [data/](data/) directory

## Methodology
* Exploratory Data Analysis of the dataset to understand each data feature among each other and to the labels.

* Clean the data and impute data for the significant amount of missing data in the dataset.  The data did not appear to be intentionally left out, instead it was not available when the data collection took place, or the data collection was not rigorous enough.

* The dataset is highly imbalanced, oversampling will be needed to create synthetic data to balance the clases.

* Implement Supervised Learning Classifiers. Five classifiers were implemented and the best performing had its hyperparameters tuned.  Random Forest was the best performing and the others were Logistic Regression, Logistic Regression with SMOTE oversampling, Decision Tree with SMOTE oversampling, and XGBoost with SMOTE oversampling.

## Model Performance
Performance was judged on overall accuracy and balanced recall.

After tuning the Random Forest Classifier, it had a 73% overall accuracy, and recall of the the three classes was 0.74, 0.59 and 0.74 for functional, functional needs repairs, and non-functional respectively.

## Recomendations
* Use the model to prioritize site visits.  Priority should be given to maintenance staff sent to waterpoints that are predicted to be functional but in need of repair or non functional.

* The Ministry can use the cost savings from a more efficient maintenance operation to expand the water infrastructure.

* The Ministry can use the accuracy of the model and its improved maintenance program as a selling point when soliciting international aid.

## Future Work
* **Investigate Problematic Misclassifications**: In our situation we have three classes (functional, functional needs repairs & non functional) for our waterpoints that we want to correctly classify.  We were able to get an accuracy of 73%, but can we do better and how.  In this table green indicates correct, yellow indicates wrong, but ok, and red indicates wrong, but not ok.  We need to focus on correcting the misclassifications in the red zones.  For example if a waterpoint is non-functional but is predicted as functional needs repairs, a yellow square. That is not much of a problem because the maintenance staff would visit the site and find they had to do more repairs than anticipated.  Compare that to a Non-Functional site being misclassified as functional, a red square.  In this case the waterpoint would not be visited and would remain non-functional.

* **Use Maintenance Records**: While the current models does a good job, going forward we will need additional data to keep the model up to date and improve its classification power.  One way to do this will be gathering historical maintenance records and implementing a structure for collecting them in the future so that they can be incorporated into the model.

* **Identify Useless Waterpoints**: The Random Forest Classifier found that the most important feature for classifying a waterpoint was whether it was dry, meaning regardless of the functionality of the water point there was no water.  In the dataset, dry waterpoints were almost exclusively non-functional.  An attempt should be made to train the model to further classify non-functional waterpoints as to visit or ignore.  Dry is an obvious characteristic, but a classification model may be able to determine if there are others or combinations of others, to assist in further optimizing waterpoint maintenance operations.

## For Further Information
Please review the narrative of the analysis in the [Jupyter notebooks](index.ipynb) or review the [presentation](tanzanian_water_wells.pdf).
