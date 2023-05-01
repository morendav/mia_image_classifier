
# Membership Inference Attack case study in Python

ML models are capable of memorizing training examples, or samples from the dataset used to train the neural networks
Membership Inference Attacks (MIA) are a type of model analysis that allow us to measure how much advantage an attacker has when trying to guess whether a particular example was part of the training dataset or not.

This case study demonstrates the MIA over a set of experiments for comparison of results. For all experiments the CIFAR10 dataset is used, credit due to TensorFlow dataset library for making this dataset publicly available.
The experiments are comparisons:
1. Between two models of different architectures
   * a convolutional neural net (NN) is compared to a densely connected NN
   * both models are of equal depth, however note the models have very different trainable parameter counts
   * Demonstrates different model types and memorization rates, as well as sets a baseline for following experiments
2. Between two models of different depths
   * both models are densely connected NN of depth 7 and 4, thus having nearly 2x more parameters in the larger
   * Demonstrates the affect of having more parameters / deeper NN has on memorization rates
3. Experiment 2 is repeated for a truncated dataset
   * the same CIFAR10 is used, however only the first 4 classes of the 10 class dataset are used for these models
   * Demonstrates the affect of classificaiton output entropy has on memorization rates


## TODO - FINISH README

## mia.py

### Outline
Methods to repeatedly run private statistic generation. Arguments: number of iterations, data (list), privacy budget (epsilon)
* repeated_sum
* repeated_average
* repeated_max

Class to import data from csv, and clean the data
Class methods to generate nonprivate statistic (mean, max, sum)

Code in _main_
* initalize class of clean data from csv
* makes use of repeated_averaage and class method prepareData.nonprivate_average
* generates plots for the study




### Ouput

Running laplace.py as written generates a set of 4 figures:

* annual_income_distribution_plots.png
  * histograms and boxplots of the unmodified source data, demonstrating significant right-skew of the data
  * note: a plot in this series is in log scale, so as to fully appreciate the skewness of the data
* repeated_average_historgram.png
  * observations of repeated private queries on the unmodified source data (e.g. private average)
  * note: center of observations fall on true value
* skew_corrected_repeated_average_historgram.png
  * observations of repeated private queries on the skew-corrected source data
* normalized_noise_observations.png
  * Observations for skew-crrected and unmodified (skewed) data
  * observations in this series are normalized with respect to each source data's true metric (e.g. true average)



### Input

Data is provided in the /data/*.csv files located in the project root directory.
This data was sourced from [Kaggle: Credit Score Classification](https://www.kaggle.com/datasets/parisrohan/credit-score-classification) challenge and carries an [Universal, Creative Commons Public License](https://creativecommons.org/publicdomain/zero/1.0/)

This data is a fictional dataset that presents a unique user id keyed credit scoring source data. For the purpose of this demonstartion the annualized salary for the last month of the year (month = december) is used.


## Software License

[Apache License 2.0](https://choosealicense.com/licenses/apache-2.0/)