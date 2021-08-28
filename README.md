# Credit Line Increase Model Card

### Basic Information

* **Person or organization developing model**: Jospehine Yang, `yangxiaoda@gwmail.gwu.edu`
* **Model date**: August, 2021
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [6301_project.ipynb](6301_project.ipynb)

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
* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None

### Model Details
* **Columns used as inputs in the final model**:x_names
* **Column(s) used as target(s) in the final model**:y_name
* **CType of model**:Decision Tree
* **CSoftware used to implement the model**:Python
* **CVersion of the modeling software**:0.22.2.post1
* **CHyperparameters or other settings of your model**:DecisionTreeClassifier(ccp_alpha=0.0, class_weight=None, criterion='gini',
                       max_depth=6, max_features=None, max_leaf_nodes=None,
                       min_impurity_decrease=0.0, min_impurity_split=None,
                       min_samples_leaf=1, min_samples_split=2,
                       min_weight_fraction_leaf=0.0, presort='deprecated',
                       random_state=12345, splitter='best')
###  Quantitative Analysis
* **Metrics used to evaluate your final model**:AUC python
* **State the final values of the metrics for all data: training, validation, and test data**:
Training AUC: 0.78 Validation AUC: 0.75 Test AUC: 0.74 Asian-to-White AIR: 1.00 Black-to-White AIR: 0.85 Female-to-Male AIR: 1.02 Hispanic-to-White AIR: 0.83
* **Provide any plots related to your data or final model -- be sure to label the plots!**:

### Ethical considerations (6 pts.):
* **Describe potential negative impacts of using your model**:Variable importance"
   *Math or software problems**:In recalculation result, the ratio of giving credit extention for hispanic to white 0.83:1 ,which means that for every 1000 white people receive credit extention, only 830 hispanic people could get the same treatment. This could not be completely avoided, but we can tried to improve this. 
   *Real-world risks: who, what, when or how**:In real world, the credit extension difference among different groups of people will be enlarged as the population base grows larger. Then the fairness and parity issues would be enlarged while using this model. 
* **Describe potential uncertainties relating to the impacts of using your model**:
   *Math or software problems**:the "pay_0" variable is extremely important based on its position on the graph of "Variable importance". The trend on ""Variable Importance" graphy is quite sharp that could cause quite big change on result once any tiny bit change on the "pay_0" variable.
   *Real-world risks: who, what, when or how?: Firstly, this would cause consumers' privacy problem. Secondly, the "pay_0" variable is the data about consumers' latest payment status, and the accuracy of this variable highly depends on the steady of the econnomic situation. 
* **Describe any unexpected or results**
   *The economic situation is highly unpredictable. Therefore once there's anything change on economic situation, it would seriously impact on this variable and the accuracy of the result from this variable.
