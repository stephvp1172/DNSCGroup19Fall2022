#
# **Credit Line Increase Model Card**

### **Basic Information**

- **Persons developing model** : Stephanie Palanca ([spalanca8@gwmail.gwu.edu](mailto:spalanca8@gwmail.gwu.edu)), Wanting Liu ([wantingl114@gwmail.gwu.edu](mailto:wantingl114@gwu.edu)), Jiahui Chen ([jiahui.chen@gwmail.gwu.edu](mailto:jiahui.chen@gwmail.gwu.edu)), Yifan Li (yifan.li1@gwmail.gwu.edu)
- **Model date** : August, 2022
- **Model version** : 1.0
- **License** : MIT License
- **Project GitHub Page:** [Model GitHub Page](https://github.com/stephvp1172/DNSCGroup19Fall2022)
- **Model implementation code** : [DNSC\_6301\_Example\_Project.ipynb](https://github.com/stephvp1172/DNSCGroup19Fall2022/blob/main/DNSC_6301_Project_Group_19.ipynb)
- **Intended Use**
  - **Primary intended uses**: This model is an _example_ probability of default classifier, with an _example_ use case for determining eligibility for a credit line increase.
  - **Primary intended users**: Students in GWU DNSC 6301 bootcamp.
  - **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### **Training Data**

- **Source of training data** : GWU Blackboard, email jphall@gwu.edu for more information
- **How training data was divided into training and validation data** : 50% training, 25% validation, 25% test
- **Number of rows in training and validation data** :
  - Training rows: 15,000
  - Validation rows: 7,500
- **Data dictionary** :

| **Name** | **Modeling Role** | **Measurement Level** | **Description** |
| --- | --- | --- | --- |
| ID | ID | int | Unique row indentifier |
| LIMIT\_BAL | input | float | Amount of previously awarded credit |
| SEX | Demographic information | int | 1 = male; 2 = female |
| RACE | Demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| EDUCATION | Demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| MARRIAGE | Demographic information | int | 1 = married; 2 = single; 3 = others |
| AGE | Demographic information | int | Age in years |
| PAY\_0, PAY\_2 - PAY\_6 | Inputs | int | History of past payment; PAY\_0 = the repayment status in September, 2005; PAY\_2 = the repayment status in August, 2005; ...; PAY\_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| BILL\_AMT1 - BILL\_AMT6 | Inputs | float | Amount of bill statement; BILL\_AMNT1 = amount of bill statement in September, 2005; BILL\_AMT2 = amount of bill statement in August, 2005; ...; BILL\_AMT6 = amount of bill statement in April, 2005 |
| PAY\_AMT1 - PAY\_AMT6 | Inputs | float | Amount of previous payment; PAY\_AMT1 = amount paid in September, 2005; PAY\_AMT2 = amount paid in August, 2005; ...; PAY\_AMT6 = amount paid in April, 2005 |
| DELINQ\_NEXT | Target | int | Whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

### **Test Data**

- **Source of test data** : GWU Blackboard, email jphall@gwu.edu for more information
- **Number of rows in test data** : 7,500
- **State any differences in columns between training and test data** : None

### **Model details**

- **Columns used as inputs in the final model** : 'LIMIT\_BAL', 'PAY\_0', 'PAY\_2', 'PAY\_3', 'PAY\_4', 'PAY\_5', 'PAY\_6', 'BILL\_AMT1', 'BILL\_AMT2', 'BILL\_AMT3', 'BILL\_AMT4', 'BILL\_AMT5', 'BILL\_AMT6', 'PAY\_AMT1', 'PAY\_AMT2', 'PAY\_AMT3', 'PAY\_AMT4', 'PAY\_AMT5', 'PAY\_AMT6'
- **Column(s) used as target(s) in the final model**: 'DELINQ\_NEXT'
- **Type of model** : Decision Tree
- **Software used to implement the model** : Python, scikit-learn
- **Version of the modeling software** : Python version: 3.7.13; scikit-learn version: 1.0.2
- **Hyperparameters or other settings of your model** :

{'ccp\_alpha': 0.0,

'class\_weight': None,

'criterion': 'gini',

'max\_depth': 6,

'max\_features': None,

'max\_leaf\_nodes': None,

'min\_impurity\_decrease': 0.0,

'min\_samples\_leaf': 1,

'min\_samples\_split': 2,

'min\_weight\_fraction\_leaf': 0.0,

'random\_state': 12345,

'splitter': 'best'}

### **Quantitative Analysis**

- **Metrics used to evaluate your final model (AUC and AIR)**
  - AUC (Area Under the Curve) - This shows us the measurements for the entire area under the ROC curve. The AUC provides us with a measure of the performance of our model when given the tree depth. 
  - AIR (Adverse Impact Ratio) - This is a metric of discrimination that shows us what is the rate of positive outcomes for protected groups to the rate of protected outcomes for our controlled group.

- **State the final values**

|  | **Training** | **Validation** | **Test** |
|---|---|---|---|
| **AUC** | 0.783722 | 0.749610 | 0.7438 |

|  | **Hispanic-to-White** | **Black-to-White** | **Asian-to-White** | **Female-to-Male** |
|---|---|---|---|---|
| **AIR (Before Cutoff)** | 0.76 | 0.82 | 1.00 | 1.06 |
| **AIR (After Cutoff)** | 0.83 | 0.85 | 1.00 | 1.02 |

Among the 12 depth models we have trained, the best performing model is when the depth equals to 6 since it has the highest Validation AUC and the second highest Training AUC and AIR.

- **Plots related to your data or final model**
  - Iteration Plot

As shown in the plot, the maximum of the Validation AUC is on depth 6, and the AIR reaches highest (except for the depth 1) when it is depth 6 or 7. Therefore, depth 6 might be the best model.


![iteration plot](https://user-images.githubusercontent.com/111540054/187085357-0b09d05a-350d-4240-a859-5b5561c1a3b2.png)


  - Iteration Table

As shown in the table, the Validation AUC reaches its maximum number and Air is almost its maximum number when depth is 6.
|  | **Training AUC** | **Validation AUC** | **5-Fold SD** | **Hispanic-to-White AIR** |
|---|---|---|---|---|
|1|0\.6457482959813234|0\.6438801727855158|0\.009275303818023868|0\.89414802613357|
|2|0\.6999123398719492|0\.6877515174864963|0\.012626349411887162|0\.8508708566822412|
|3|0\.7429683381846597|0\.7294904970517769|0\.017374757121649664|0\.7995458049063263|
|4|0\.7571782808596749|0\.7416959617891924|0\.017078668660042047|0\.7924351307435884|
|5|0\.769330591573498|0\.7424798752841699|0\.019885824829898823|0\.8293357260617733|
|6|0\.7837218463585236|0\.7496104671485542|0\.01766546815507475|0\.8332051458797409|
|7|0\.7957771914330948|0\.7421151172017523|0\.02246572082370893|0\.8358864398209704|
|8|0\.8072906197591377|0\.7399900492688766|0\.015566659969458982|0\.8112997077549317|
|9|0\.8229130088551059|0\.7272242307957267|0\.012041631852087134|0\.8115607234254505|
|10|0\.8380519590210705|0\.72056249697013|0\.013854894144390251|0\.8036206182597267|
|11|0\.8551676678431094|0\.7098641342481202|0\.010404527126885185|0\.8378061717569955|
|12|0\.8742507449104165|0\.688074125292462|0\.008073026747413463|0\.8448891638378985|

  - Histogram

It can be easily seen that the distribution of variables. For example, most people pay their bill on-time based on the graph of the DELINQ\_NEXT graph at the end.

![histogram](https://user-images.githubusercontent.com/111540054/187085372-0507ad7d-eda6-434d-92bc-0a3a55a7eb85.png)



  - Correlation Heatmap

To see the correlationship between variables. For example, RACE and DELINQ\_NEXT are negatively correlated.


![heatmap](https://user-images.githubusercontent.com/111540054/187085385-68b0c12a-3488-4c44-ad04-e1ce24dba8ab.png)


  - Variable Importance

The chart below shows us that we are relying too heavily on September (PAY\_0) information, as it has a significantly higher variable importance than all other inputs.


![variable importance](https://user-images.githubusercontent.com/111540054/187085396-eb2477fd-3461-44ee-90d4-b06e9d21adf5.png)



## **Ethical Considerations:**

- **Potential Negative Impacts and Uncertainties**
  - **Math/Software Issues**
    - Because there are thousands of different good decision making models (Rashomon effect), our data can change with the slightest tweek. This means there are thousands of possibilities, and would be impossible for us to try them all.
    - Our test data is relatively small since there are only 7,500 rows. This means that we were not able to run difficult tests on the model, so this model may not give us an accurate prediction of future credit payments.
  - **Real World Risks**
    -  Demographic information, such as race and gender, pose both a privacy issue for consumers and it can cause our own biases to get in the way of creating a truly unbias model. This can quickly become an issue of disparate treatment, as our model can make decisions based on a consumer's sex or race.  Bias tests reveal certain demographic groups, like Black or Hispanic people, may be experiencing disparate impact under this model, which can lead to legal and reputation ramifications for the company.
    -  The initial AIR for hispanic-to-white was less than 0.8 (0.76). This required us to modify the cutoffs in order to increase that number. 
- **Negative/Unexpected Results**
    - This data set also had no missing values. This is unrealistic to real world scenarios, as datasets we will work with in the future may contain missing values.
    - The model relies too much on September's data (PAY\_0). This means that if September's data is inaccurate, it will negatively affect the accuracy of the whole model.
