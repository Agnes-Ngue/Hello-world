# Credit Line Increase Model Card

# Basic Information

•Person or organization developing model: Agnes Danielle Flore Nguenda, agnesdanielleflore.nguenda@gwmail.gwu.edu

• Model date: August, 2022

• Model version: 1.0

• License: MIT

• Model implementation code: DNSC_6301_Example_Project.ipynb

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
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
| Name      | Modeling Role  | Measurement Level | Description                                     |
