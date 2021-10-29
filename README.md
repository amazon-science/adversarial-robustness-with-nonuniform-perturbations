# Adversarial Robustness with Non-uniform Perturbations
This repository hosts the code to replicate experiments of the paper Adversarial Robustness with Non-uniform Perturbations for malware use-case. 

## Installation
Please first refer to https://github.com/elastic/ember and follow the instructions to download 2018 version of EMBER dataset and install `ember` package.

After installing `ember`, use `pip` to install the required packages for this project:
```
pip install -r requirements.txt
```

## Usage
### NonuniformRobustness.py
This file contains the following functions:

- `get_clean_data(data_dir)` returns train and test sets of vectorized EMBER dataset features

- `get_adversarial_examples(data_dir, num_features, attack_name="GreedyNN")` returns adversarial example set which is 
crafted by the specified problem space attack, e.g., Greedy attack (GreedyNN). 

- `omega(num_features, perturbation_constraint="Uniform")` computes the matrix Omega which is used in l2 PGD algorithm 
as a coefficient of delta perturbation constraint. Constraint type can be selected as `"Uniform"`, `"Pearson"`,
`"SHAP"`,`"Masked"`,`"Mahalanobis"` and `"Mahalanobis benign"`.

- `pgd_l2(model, X, y, config)` returns delta perturbations to be added to training data during adversarial training. 
l2 PGD algorithm is applied according to the given configurations which contain `omega` matrix of previously selected
`perturbation_constraint`.

- `get_trained_model` returns adversarially trained model with l2 PGD algorithm and prints test performance on clean 
data and adversarial examples

### Malware_demo.ipynb
Contains a demo of adversarial training a model with specified perturbation constraints. Clean accuracy on test set and 
defense success on adversarial examples are tested.

### nonuniform_omega
Contains necessary data for Omega matrix calculation such as Pearson correlation coefficients, Shapley values, 
covariance matrix of the training set to calculate Mahalanobis distance and covariance matrix of only benign class for 
Mahalanobis benign.

### Adversarial_example_sets
Contains the adversarial example sets generated by the [winner attacks](https://towardsdatascience.com/evading-machine-learning-malware-classifiers-ce52dabdb713) of malware evasion competition 2019.