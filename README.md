## 1. Resampling Imbalanced Data

In practice, you will encounter imbalanced data more often than not. This does not necessarily have to be a problem if your target only has a slight imbalance. 

You could then resolve it by using proper validation measures for the data such as Balanced Accuracy, Precision-Recall Curves or F1-score.

Unfortunately, this is not always the case and your target variable might be highly imbalanced (e.g., 10:1). 

Instead, **Use SMOTE algorithm from 6 effective ways to handle imbalanced classes**
#### 1. Up-sample Minority Class
- You can read about it [Here](https://elitedatascience.com/imbalanced-classes)
#### 2. Down-sample Majority Class
- You can read about it [Here](https://elitedatascience.com/imbalanced-classes) 
#### 3. Change Your Performance Metric
- we recommend Area Under ROC Curve (AUROC). You can read more about it [Here](https://stats.stackexchange.com/questions/132777/what-does-auc-stand-for-and-what-is-it)
#### 4. Penalize Algorithms (Cost-Sensitive Training)
- its increase the cost of classification mistakes on the minority class.A popular algorithm for this technique is Penalized-SVM
- model = SVC(kernel='linear', class_weight='**balanced**',probability=True) # penalize-balanced
#### 5. Use Tree-Based Algorithms
- Decision trees often perform well on imbalanced datasets because their hierarchical structure allows them to learn signals from both classes.
#### 6. SMOTE Method
- SMOTE (synthetic minority oversampling technique) is one of the most commonly used oversampling methods to solve the imbalance problem.used to increase the samples in a minority class.
- It generates new samples by looking at the feature space of the target and detecting nearest neighbors. Then, it simply selects similar samples and changes a column at a time randomly within the feature space of the neighboring samples.
- The module to implement SMOTE can be found within the imbalanced-learn package. You can simply import the package and apply a fit_transform:


<img align="center" alt="Coding" width="400" src="https://github.com/connectkishan1/feature-engineering/blob/master/distribution.png"><img align="center" alt="Coding" width="400" src="https://github.com/connectkishan1/feature-engineering/blob/master/resampled.png">

- As you can see the model successfully oversampled the target variable. There are several strategies that you can take when oversampling using SMOTE:

1. 'minority': resample only the minority class;
2. 'not minority': resample all classes but the minority class;
3. 'not majority': resample all classes but the majority class;
4. 'all': resample all classes;

- When dict, the keys correspond to the targeted classes. The values correspond to the desired number of samples for each targeted class.
- I chose to use a dictionary to specify the extent to which I wanted to oversample my data.

- Additional tip 1: If you have categorical variables in your dataset SMOTE is likely to create values for those variables that cannot happen. For example, if you have a variable called isMale, which could only take 0 or 1, then SMOTE might create 0.365 as a value.

- Instead, you can use SMOTENC which takes into account the nature of categorical variables. This version is also available in the imbalanced-learnpackage.

- Additional tip 2: Make sure to oversample after creating the train/test split so that you only oversample the train data. You typically do not want to test your model on synthetic data.

