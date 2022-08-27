# Credit Line Increase Model Card

### Basic Information

* **Person or organization developing model**: Agnes, `agnes@gmc.com`

* **Model date**: August, 2022

* **Model version**: 1.0.2

* **License**: MIT

* **Model implementation code**: [DNSC_6301_Project.ipynb](https://github.com/Agnes-Ngue/Hello-world/blob/main/GWU_DNSC_6301_project.ipynb)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: Students in GWU DNSC 6301 bootcamp.
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.
                       




### Training Data

* Data dictionary:

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

* **Source of training data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

    
    
### Test Data

* **Source of test data**: GWU Blackboard, email jphall@gwu.edu for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None



### Model details


* **Columns used as inputs in the final model**: 'LIMIT_BAL',
       'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1',
       'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6',
       'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'
* **Column(s) used as target(s) in the final model**: 'DELINQ_NEXT'
* **Type of model**: Decision Tree 
* **Software used to implement the model**: Python, scikit-learn
* **Version of the modeling software**: 3.7.13, 1.0.2
* **Hyperparameters or other settings of your model**: 
```
DecisionTreeClassifier  {'ccp_alpha': 0.0,'class_weight': None,'criterion': 'gini',
                         'max_depth': 12,'max_features': None,'max_leaf_nodes': None,
                         'min_impurity_decrease': 0.0,'min_samples_leaf': 1,'min_samples_split': 2,
                         'min_weight_fraction_leaf': 0.0,'random_state': 12345,'splitter': 'best'}
```

### Quantitative Analysis

#### Correlation Heatmap

![image](https://user-images.githubusercontent.com/111556214/186575609-18b8e494-6bb5-48b7-9eef-2b818c1081cc.png)

Wider colors = positively correlated

darker colors = negatively correlated

So, when one variable goes up the other one goes down

i.e : there is a correlation between race and the outcome. There is a problem to figure out and fix.

This means people in certain race groups are not getting as many as other people

strong correlation between variables

* **Metrics used to evaluate your final model (AUC and AIR)**: confusion matrix

#### confusion matrices across race groups
```
Confusion matrix by RACE=1

                actual: 1 actual: 0
     predicted: 1       447       387
     predicted: 0       139       501
     (Hispanic)

Confusion matrix by RACE=2
             actual: 1 actual: 0
predicted: 1       449       348
predicted: 0       157       537
(Black)


Confusion matrix by RACE=3
             actual: 1 actual: 0
predicted: 1       176       813
predicted: 0        72      1228
(White)


Confusion matrix by RACE=4
             actual: 1 actual: 0
predicted: 1       186       784
predicted: 0        59      1217
(Asian)


White proportion accepted: 0.568
Hispanic proportion accepted: 0.434
hispanic-to-white AIR: 0.76

White proportion accepted: 0.568
Black proportion accepted: 0.465
black-to-white AIR: 0.82

White proportion accepted: 0.568
Asian proportion accepted: 0.568
asian-to-white AIR: 1.00
```



#### confusion matrices across sex groups


```
Confusion matrix by SEX=1
             actual: 1 actual: 0
predicted: 1       546       905
predicted: 0       179      1292
(Male)


Confusion matrix by SEX=2
             actual: 1 actual: 0
predicted: 1       712      1427
predicted: 0       248      2191
(Female)


Male proportion accepted: 0.503
Female proportion accepted: 0.533
female-to-male AIR: 1.06
```






* **State the final values, neatly -- as bullets or a table, of the metrics for all data**: training, validation, and test data


||	Training AUC|	Validation AUC|	5-Fold SD|
|-|--------|------|-----|
|1|	0.645748|	0.643880|	0.009275|
|2	|0.699912|	0.687752	|0.012626|
|3|	0.742968	|0.729490	|0.017375|
|4|	0.757178	|0.741696|	0.017079|
|5|	0.769331|	0.742480|	0.019886|
|6|	0.783722|	0.749610|	0.017665|
|7|	0.795777|	0.742115|	0.022466|
|8|	0.807291|	0.739990|	0.015567|
|9|	0.822913|	0.727224|	0.012042|
|10	|0.838052|	0.720562|	0.013855|
|11	|0.855168|	0.709864|	0.010405|
|12|	0.874251|	0.688074|	0.00807|



* Provide any plots related to your data or final model -- be sure to label the plots!

#### plot tree depth vs. training and validation AUC and AIR

![image](https://user-images.githubusercontent.com/111556214/186954891-8919e73c-1563-45c7-84ad-fe44015a877f.png)



### Ethical considerations

* Describe potential negative impacts of using your model:

   * Math or software problems: 70% accuracy rate, which means a 30% errors 
   
   * Real-world risks: who, what, when or how: bias 
   
* Describe potential uncertainties relating to the impacts of using your model:
 
   * Math or software problems: need for ongoing monitoring as we don't know how the model will function 
   * Real-world risks: who, what, when or how? Data privacy and security  
*  Describe any unexpected or results: no missing values and PAY_0 being too important
