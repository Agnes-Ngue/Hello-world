# Credit Line Increase Model Card

# Basic Information

•Person or organization developing model: Agnes Danielle Flore Nguenda, agnesdanielleflore.nguenda@gwmail.gwu.edu

• Model date: August, 2022

• Model version: 1.0.2

• License: MIT

• Model implementation code: [DNSC_6301_Project.ipynb](https://github.com/Agnes-Ngue/Hello-world/blob/main/GWU_DNSC_6301_project.ipynb)

• Information about training algorithms, parameters, fairness constraints or other applied approaches, and features

• Paper or other resource for more information

• Citation details

• Where to send questions or comments about the model


# Model details


• Columns used as inputs in the final model: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'

• Column(s) used as target(s) in the final model: 'DELINQ_NEXT'

• Type of model: Decision Tree

• Software used to implement the model: Python, scikit-learn

• Version of the modeling software: 0.22.2.post1

• Hyperparameters or other settings of your model:

    DecisionTreeClassifier   (ccp_alpha=0.0, class_weight=None, criterion='gini',
                             max_depth=6, max_features=None, max_leaf_nodes=None,
                             min_impurity_decrease=0.0, min_impurity_split=None,
                             min_samples_leaf=1, min_samples_split=2,
                             min_weight_fraction_leaf=0.0, presort='deprecated',
                             random_state=12345, splitter='best')`
                       



# Intended Use

• Primary intended uses: This model is an example probability of default classifier, with an example use case for determining eligibility for a credit line increase.

• Primary intended users: Students in GWU DNSC 6301 bootcamp.

• Out-of-scope use cases: Any use beyond an educational example is out-of-scope.


# Training Data

• Data dictionary:

| Name      | Modeling Role            | Measurement Level | Description                                     |
|-----------|--------------------------|-------------------|-------------------------------------------------|
| ID        | ID                       | int               | unique row indentifier                          |
| LIMIT_BAL | input                    | float             | amount of previously awarded credit             |
| SEX       | demographic information  | int               | 1 = male; 2 = female                            |
| RACE      | demographic information  | int               | 1 = hispanic; 2 = black; 3 = white; 4 = asian   |
| EDUCATION | demographic information  | int               | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| MARRIAGE  | demographic information  | int               | 1 = married; 2 = single; 3 = others             |
| AGE       | demographic information  | int               | age in years                                    |
|PAY_0, PAY_2 - PAY_6     | inputs                   | int        | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| BILL_AMT1 - BILL_AMT6    | inputs  | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005           |
| PAY_AMT1 - PAY_AMT6     | inputs  | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005                                    |
| DELINQ_NEXT    | target  | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time                                       |

• Source of training data: GWU Blackboard, email jphall@gwu.edu for more information


• How training data was divided into training and validation data: 50% training, 25% validation, 25% test


• Number of rows in training and validation data:

    * Training rows: 15,000
    
    * Validation rows: 7,500
    
# Load and analyze data 

• Names of the columns in the training data

        Index(['ID', 'LIMIT_BAL', 'SEX', 'RACE', 'EDUCATION', 'MARRIAGE', 'AGE',
               'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1',
               'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6',
               'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6',
               'DELINQ_NEXT'],
              dtype='object')

• Determine whether any missing values exist in the training data: 'there are no missing values'

• basic descriptive statistics for the data  

|index|ID|LIMIT\_BAL|SEX|RACE|EDUCATION|MARRIAGE|AGE|PAY\_0|PAY\_2|PAY\_3|PAY\_4|PAY\_5|PAY\_6|BILL\_AMT1|BILL\_AMT2|BILL\_AMT3|BILL\_AMT4|BILL\_AMT5|BILL\_AMT6|PAY\_AMT1|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|count|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|
|mean|15000\.5|167484\.32266666667|1\.6037333333333332|2\.721966666666667|1\.8531333333333333|1\.5518666666666667|35\.4855|-0\.0167|-0\.13376666666666667|-0\.1662|-0\.22066666666666668|-0\.2662|-0\.2911|51223\.3309|49179\.07516666667|47013\.1548|43262\.94896666666|40311\.40096666667|38871\.7604|5663\.5805|
|std|8660\.398374208891|129747\.66156720239|0\.48912919609026045|1\.0943966628653183|0\.7903486597207291|0\.5219696006132486|9\.217904068090188|1\.1238015279973348|1\.1971859730345533|1\.1968675684465735|1\.1691386224023375|1\.1331874060027483|1\.1499876256079027|73635\.86057552956|71173\.76878252835|69349\.38742703684|64332\.85613391631|60797\.15577026487|59554\.10753674573|16563\.280354025766|
|min|1\.0|10000\.0|1\.0|1\.0|0\.0|0\.0|21\.0|-2\.0|-2\.0|-2\.0|-2\.0|-2\.0|-2\.0|-165580\.0|-69777\.0|-157264\.0|-170000\.0|-81334\.0|-339603\.0|0\.0|
|25%|7500\.75|50000\.0|1\.0|2\.0|1\.0|1\.0|28\.0|-1\.0|-1\.0|-1\.0|-1\.0|-1\.0|-1\.0|3558\.75|2984\.75|2666\.25|2326\.75|1763\.0|1256\.0|1000\.0|
|50%|15000\.5|140000\.0|2\.0|3\.0|2\.0|2\.0|34\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|22381\.5|21200\.0|20088\.5|19052\.0|18104\.5|17071\.0|2100\.0|
|75%|22500\.25|240000\.0|2\.0|4\.0|2\.0|2\.0|41\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|67091\.0|64006\.25|60164\.75|54506\.0|50190\.5|49198\.25|5006\.0|
|max|30000\.0|1000000\.0|2\.0|4\.0|6\.0|3\.0|79\.0|8\.0|8\.0|8\.0|8\.0|8\.0|8\.0|964511\.0|983931\.0|1664089\.0|891586\.0|927171\.0|961664\.0|873552\.0|


• Calculate a Pearson correlation matrix for the data (2 pts.)

• Plot histograms for all the columns in the data (2 pts.)

# Test Data

• Source of test data: GWU Blackboard, email jphall@gwu.edu for more information

• Number of rows in test data: 7,500

• State any differences in columns between training and test data: None

# Model details

• Columns used as inputs in the final model: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'

• Column(s) used as target(s) in the final model: 'DELINQ_NEXT'

• Type of model: Decision Tree

• Software used to implement the model: Python, scikit-learn

• Version of the modeling software: 0.22.2.post1

• Hyperparameters or other settings of your model:

    DecisionTreeClassifier   (ccp_alpha=0.0, class_weight=None, criterion='gini',
                             max_depth=6, max_features=None, max_leaf_nodes=None,
                             min_impurity_decrease=0.0, min_impurity_split=None,
                             min_samples_leaf=1, min_samples_split=2,
                             min_weight_fraction_leaf=0.0, presort='deprecated',
                             random_state=12345, splitter='best')`
                       
# Quantitative Analysis

• Correlation Heatmap       

![image](https://user-images.githubusercontent.com/111556214/185877043-522d3e02-2dc6-4942-a4bb-08334c7f92f3.png)

![![image](https://user-images.githubusercontent.com/111556214/186575609-18b8e494-6bb5-48b7-9eef-2b818c1081cc.png)
]

    
