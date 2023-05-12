
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



## mia_intro_imageclassifier.py

### Outline

**Import Block**
* third party libraries
* tensorflow, tensorflow datasets
* tensorflow privacy libraries, module names imported as classes for ref later
* suppress warnings for logarithmic convergence (when running MIA)

**Methods & classes**
* Helper methods to create models, taking in as parameters model configuration
  * conv_nn_builder
  * dense_nn_builder
* Building the dataset for model training
  * dataset_builder - assumes default number of classes is 10
  * unison_shuffle_arrays - is called from the dataset builder
* PrivacyMetrics
  * callback tf class, runs the mia every EPOCH (frequency of testing set as hyperparameter in main)


**Main**

1. define some hyperparameters for the MIA experiment
2. create datasets
    * call to dataset builder is split into two calls per number of classes: first is for training, second is for validation dataset
    * set of calls repeated twice: once for 10 class and again for 4 class dataset
    * more info on dataset class truncation can be found in the 'dataset_builder' method metadata
3. Build models
    * 3 experiments where 2 models are compared in each experiment, 1 model is reused across experiments, so total 5 models initialized here
4. train models
    * call back to MIA every EPOCH
5. Print results
    * plot training and validation accuracy & loss per epoch
    * plot MIA results (two types of attacks, for two models per experiment) on same figure
    * total 2 plots per experiment, 3 experiments = 6plots total
    * save them locally (names, hardcoded)
6. plot sampling of training data




### Ouput

Running experiment creates 6 plots

* plot training and validation accuracy & loss per epoch
* plot MIA results (two types of attacks, for two models per experiment) on same figure
    


### Input

Data is provided by public tensorflow datasets api
Kudos to TFDS for supplying data for the ML community to use in tutorials and projects!

## Software License

[Apache License 2.0](https://choosealicense.com/licenses/apache-2.0/)