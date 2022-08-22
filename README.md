#
# **Credit Line Increase Model Card**

### **Basic Information**

- **Persons developing model** : Stephanie Palanca ([spalanca8@gwmail.gwu.edu](mailto:spalanca8@gwmail.gwu.edu)), Wanting Liu ([wantingl114@gwmail.gwu.edu](mailto:wantingl114@gwu.edu)), Jiahui Chen ([jiahui.chen@gwmail.gwu.edu](mailto:jiahui.chen@gwmail.gwu.edu)), Yifan Li (yifan.li1@gwmail.gwu.edu)
- **Model date** : August, 2022
- **Model version** : 1.0
- **License** : MIT License
- **Project GitHub Page:** [Model GitHub Page](https://github.com/jphall663/GWU_DNSC_6301_project)
- **Model implementation code** : [DNSC\_6301\_Example\_Project.ipynb](https://github.com/stephvp1172/DNSCGroup19Fall2022/blob/main/Copy_of_DNSC_6301_Example_Project.ipynb)
- **Intended Use**
  - **Primary intended uses** :
    - Train a Decision Tree model to predict whether or not customers will pay their next month credit card bill on-time.
    - This model is used to predict the probability of whether or not consumers will pay their credit cards on time next month, and whether or not they are eligible for a credit line increase.
  - **Primary intended users** : Professor and students in GWU DNSC 6301 Bootcamp.
  - **Out-of-scope use cases** : Everything beyond the primary intended use stated above is out-of-scope.

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

DecisionTreeClassifier(ccp\_alpha=0.0, class\_weight=None, criterion='gini',

max\_depth=6, max\_features=None, max\_leaf\_nodes=None,

min\_impurity\_decrease=0.0, min\_impurity\_split=None,

min\_samples\_leaf=1, min\_samples\_split=2,

min\_weight\_fraction\_leaf=0.0, presort='deprecated',

random\_state=12345, splitter='best')`

### **Quantitative Analysis**

- **Metrics used to evaluate your final model (AUC and AIR)**
  - **AUC (Area Under the Curve) -** This shows us the measurements for the entire area under the ROC curve (see definition below). The AUC provides us with a measure of the performance of our model when given the tree depth.
    - Training AUC - This AUC that we found while testing our model. To find the best model, the Validation AUC should be the maximum number. The Validation AUC ensures our model will not go too far. Therefore, our best fit model is when depth equals to 6 in this case.
    - ROC (receiver operating characteristic curve) - This graph shows us the performance of our classification model. (It is the validation AUC shown in the Iteration Plot below)
  - AIR - xxx
- **State the final values, neatly -- as bullets or a table, of the metrics for all data: training, validation, and test data**

Among the 12 depth model we have trained, the best performing model is when the depth equals to 6. When the depth is 6, the training AUC is 0.783722, validation AUC is 0.749610, and the test AUC is 0.7438. The model is a stable model when depth is 6 since the standard deviation is around 2%. Therefore, It is a good model when depth equals to 6.

- **Provide any plots related to your data or final model**
  - Iteration Plot

![](RackMultipart20220822-1-4him6w_html_e6a915d04e5151f.png)

  - Iteration Table

![](RackMultipart20220822-1-4him6w_html_bdc1ea6c75b6198c.png)

  - Histogram

![](RackMultipart20220822-1-4him6w_html_dc273fadbc49aabe.png)

  - Correlation Heatmap

![](RackMultipart20220822-1-4him6w_html_2a3a1de6b46c3a68.png)

  - Variable Importance

![](RackMultipart20220822-1-4him6w_html_3b41ee412ee6db70.png)

**Ethical Considerations:**

- **Potential Negative Impacts and Uncertainties**
  - **Math/Software Issues**
    - Because there are thousands of different good decision making models (rashmond effect), or data can change with the slightest tweek. This means there are thousands of possibilities, which would be impossible for us to try within our time constraints for this deliverable.
    - Since our test data only contains 7,500 rows, our test data is relatively small. The small number of rows meant that we were not able to run difficult tests on the model. Because of this, it is not an accurate representation, and will not give us an accurate prediction of future credit payments.
    - This data set also had no missing values. This is unrealistic to real world scenarios, as most datasets we will work with in the future will contain missing values.
    - The model relies too much on September's data (PAY\_0). This means that if September's data is inaccurate, it will negatively affect the accuracy of the whole model.
  - **Real World Risks**
    - Because we can see certain demographic information about each person, it can cause our own biases to get in the way of creating a truly unbiased model.
      - Furthermore, showing demographics such as race and gender pose an issue with privacy for consumers.
      - This can quickly become an issue of disparate treatment, as our model can make decisions based on a consumer's sex or race. This can lead to reputation problems for a company, legal ramifications, etc.
    - The data shows us that most people pay their credit card bills on time. Since this is unrealistic in the real world, the test data is imbalanced as most people do not pay their credit card bills on time every month.
- **Negative/Unexpected Results**
  - **Did we see any unexpected results?**
    - Unexpectedly (as mentioned above), the test data showed us that most consumers paid their credit card bills on time.
