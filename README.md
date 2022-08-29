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

```
Variables have a negative correlation because they move in opposite direction. 

Please polish: One sentence description, Wider colors = positively correlated, darker colors = negatively correlated, So, when one variable goes up the other one goes down, i.e : there is a correlation between race and the outcome. There is a problem to figure out and fix. This means people in certain race groups are not getting as many as other people.


#### Iteration plot tree depth vs. training and validation AUC, and AIR

![image](https://user-images.githubusercontent.com/111556214/187081025-9ac59e61-a76d-4a03-a3ba-8f1734aac09b.png)

Please polish: One sentence description, depth-6 tree is a good trade-off between best validation performance and best fairness.

* Best Model AUC:

| Training AUC | Validation AUC | Test AUC |
|--------------|----------------|----------|
| 0.783722| 0.749610 | 0.743847 |

* Best Model AIR:

| Hispanic-to-White AIR | Black-to-White AIR | Asian-to-White AIR | Female-to-Male AIR |
|-----------------------|--------------------|--------------------|--------------------|
| | | | |

### Ethical considerations

* Describe potential negative impacts of using your model:

   * Math or software problems: Please polish: One sentence description, 70% accuracy rate, which means a 30% errors
  
   * Real-world risks: who, what, when or how: Please polish: One sentence description, bias
  
* Describe potential uncertainties relating to the impacts of using your model:

   * Math or software problems: Please polish: One sentence description, need for ongoing monitoring as we don't know how the model will function
  
   * Real-world risks: who, what, when or how? Please polish: One sentence description, Data privacy and security 
  
*  Describe any unexpected or results: Please polish: One sentence description, no missing values and PAY_0 being too important










### Ethical considerations

* Describe potential negative impacts of using your model:

   * Math or software problems: the higher the cut off is less discriminatory, the higher is the accuracy. So, for example having a 70% accuracy rate, which means a 30% errors, and less discrimination. 
   
   * Real-world risks: who, what, when or how: Withe a cutoff less than 0.18, less Hispanic and black people will get the credit product.bias 
   
* Describe potential uncertainties relating to the impacts of using your model:
 
   * Math or software problems: need for ongoing monitoring as we don't know how the model will function 
   * Real-world risks: who, what, when or how? Data privacy and security  
*  Describe any unexpected or results: no missing values and PAY_0 being too important
