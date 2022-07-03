# Responsible_Machine_Learning
Content

**Intended use**

- Primary intended uses:
  - To predict whether or not the annual percentage rate (APR) charged for a mortgage is 150 basis points (1.5%) or more above a survey-based estimate of similar mortgages. (High-priced mortgages are legal, but somewhat punitive to borrowers. High-priced mortgages often fall on the shoulders of minority home owners, and are one of many issues that perpetuates a massive disparity in overall wealth between different demographic groups in the US.)
  - The intended use is also to train an interpretable machine learning model, which is transparent and helps prevent biases.
  - Primary intended users: Students and academics interested in interpretable machine learning models.
  - Out-of-scope use cases: This is solely for educational purpose. Any use beyond an educational example is out-of-scope.
- Describe the business value of your group's best remediated model
  - The best remediated model is used for Discrimination testing and attempt remediating of discovered discrimination using AIR (adverse impact ratio)
image
  - Retrained the most accurate model above 0.8 AIR
  - Best AUC: 0.7805 above 0.8 AIR (0.8083). Remediated EBM retrained with AUC: 0.7805.
  - Checked that other groups are not adversely impacted y change: Adverse impact ratio for Asian people vs. White people: 1.156. Adverse impact ratio for Black people vs. White people: 0.808. Adverse impact ratio for Females vs. Males: 0.956. This analysis shows that even with a selective cutoff of 0.17, less discriminatory models are available. The new set of features and hyperparameters leads to a ~13% increase in AIR with a ~5% decrease in AUC.
- Describe how your group's best remediated model is designed to be used
  - This will help us identify the people who are paying more for the American Dream of home ownership because of their ethinicity/gender/individual bias
- Describe the intended users for your group's best remediated model
  - All available groups have AIR above 0.8, indicating that it can be used for users from all groups(race)
- State whether your group's best remediated model can or cannot be used for any additional purposes
  - This Model can be also used to determine if the applicant can be used as sureity for someone applying for loan with no or low credit score
  - It can also be used in the Health Insurance Industry to predict if the applicant will default on premium/claims
  - It can used to evaluate disparity in Academic performances of diverse individuals/groups at University(for moderating the results to achieve fairer outcomes)
  
**Training data**

- State the source of training data
  - Home Mortgage Disclosure Act (HMDA) data in the class repository https://github.com/jphall663/GWU_rml/tree/master/assignments/data
- State how training data was divided into training and validation data
  - 70/30
- State the number of rows in training and validation data
  - Train data rows = 112253, columns = 23; and the Validation data rows = 48085, columns = 23
- Define the meaning of all training data columns
  - Data dictionary:

|Name|Modeling Role|	Measurement Level|	Description|
-----|-------------|------------------|------------|
**high_priced** |	target |	int|	whether (1) or not (0) the annual percentage rate (APR) charged for a mortgage is 150 basis points (1.5%) or more above a survey-based estimate of similar mortgages|
**conforming**|input|	int|	whether the mortgage conforms to normal standards (1), or whether the loan is different (0)|
**debt_to_income_ratio_std**|	input|	int|	standardized debt-to-income ratio for mortgage applicants|
**debt_to_income_ratio_missing**|	demographic information|	int|	missing marker (1) for debt to income ratio std
**income_std**|	input|	int|	standardized income for mortgage applicants|
**loan_amount_std**|	input|	int|	standardized amount of the mortgage for applicants|
**intro_rate_period_std**|	input|	int|	standardized introductory rate period for mortgage applicants|
**loan_to_value_ratio_std**|	input|	int|	ratio of the mortgage size to the value of the property for mortgage applicants|
**no_intro_rate_period_std**	|input|	int|	whether (1) or not (0) a mortgage does not include an introductory rate period|
**property_value_std**|	input|	int|	value of the mortgaged property|
**term_360**|	input|	int|	whether the mortgage is a standard 360 month mortgage (1) or a different type of mortgage (0)|
**male**|	demographic information|	int|	whether a person identifies as male (1) or not male (0)|
**female**	|demographic information	|int	|whether a person identifies as female (1) or not female (0)|
**black**	|demographic information|	int|	whether a person identifies as black (1) or not black (0)|
**asian**|	demographic information|	int|	whether a person identifies as asian (1) or not asian (0)|
**white**	|demographic information	|int|	whether a person identifies as white (1) or not white (0)|
**amind**	|demographic information|	int|	whether a person identifies as amind (1) or not amind (0)|
**hipac**	|demographic information	|int	|whether a person identifies as hipac (1) or not hipac (0)|
**hispanic**|	demographic information|	int|	whether a person identifies as hispanic (1) or not hispanic (0)|
**non_hispanic**	|demographic information	|int|	whether a person identifies as non_hispanic (1) or not non_hispanic (0)|
**agegte62**	|demographic information|	int	|whether a person is over the age of 62 (1) or not over the age of 62 (0)|
**agelt62E**	|demographic information	|int|	whether a person is below the age of 62 (1) or not below the age of 62 (0)|
**row_id**|	ID|	int|	unique row indentifier|

- Define the meaning of all engineered columns
  - phat and r were engineered for residual analysis.
  - phat: It is a numeric input that helps to predict probabilities of high-priced mortgage
  - r: It is a numeric input and is log loss residual for the predicted probabilities.

**Evaluation data**

- State the source of evaluation (or test) data
  - Home Mortgage Disclosure Act (HMDA) data in the class repository https://github.com/jphall663/GWU_rml/tree/master/assignments/data
- State the number of rows in evaluation (or test) data
  - 19830 (without the header). With header it is 19831
- State any differences in columns between training and evaluation (or test) data
  - There are no differences between training and evaluation (or test) data except for high_priced column included in the test data.

**Model details**

- State the columns used as inputs in your group's best remediated model
  - 'property_value_std', 'no_intro_rate_period_std', 'loan_amount_std', 'income_std', 'conforming', 'intro_rate_period_std', 'debt_to_income_ratio_std', 'term_360', 'high_priced'
- State the columns used as targets in your group's best remediated model
  - 'high_priced'
- State the type of your group's best remediated model
  - EBM
- State the software used to implement your group's best remediated model
  - 'H20', 'interpret.glassbox', 'interpret.perf', 'numpy', 'pandas', 'time', 'matplotlib.pyplot', and 'matplotlib.lines'.
- State the version of the modeling software for your group's best remediated model
  - 'h20 3.36.1.2', 'interpret 0.2.7', 'numpy 1.11.1', and 'pandas 0.19.2
- State the hyperparameters or other settings of your group's best remediated model
  - 'max_bins': 512,'max_interaction_bins': 16,'interactions': 10,'outer_bags': 4,'inner_bags': 0,'learning_rate': 0.001,'validation_size': 0.25,'min_samples_leaf': 5,'max_leaves': 5,'early_stopping_rounds': 100.0,'n_jobs': NTHREAD, 'random_state': 12345

**Quantitative analysis**

- State the metrics used to evaluate your group's best remediated model
  - AUC
- State the values of the metrics for training, validation, and evaluation (or test) data evaluation (or test) metrics come from the most recent class full evaluation results, link under Assignment 1.
  - Explainable Boosting Machine - Validation AUC 0.8249 (RANK 1); Monotonic XGBoost - Validation AUC 0.7920 (RANK 2); and Elastic Net - Validation AUC 0.7538 (RANK 3)
- Provide at least one plot or table from each weekly assignment for a total of at least six plots, that must include the global variable importance and partial dependence of your group's best remediated model.

  - Assignment 1
    <img width="591" alt="image" src="https://user-images.githubusercontent.com/89561764/177041782-870d1af9-7168-4d7c-ae96-3ae07e85448a.png">

  - Assignment 2
    <img width="1013" alt="image" src="https://user-images.githubusercontent.com/89561764/177041833-e7eb1051-7fbc-4b6f-af18-498c9c8c4818.png">

  - Assignment 3
    <img width="512" alt="image" src="https://user-images.githubusercontent.com/89561764/177041942-528a672a-603f-46d6-92fc-708ae93ea5c1.png">

  - Assignment 4
    <img width="938" alt="image" src="https://user-images.githubusercontent.com/89561764/177041977-e0f54982-b578-4049-a240-181d503f550a.png">
    
  - Assignment 5
    <img width="497" alt="image" src="https://user-images.githubusercontent.com/89561764/177042069-2b35d250-76fb-4cd8-9738-767e44e9778d.png">

- Address other alternative models considered
  - None. Only above Explainable Boosting Machine, Monotonic XGBoost and Elastic Net were considered

**Ethical considerations**

- Describe potential negative impacts of using your group's best remediated model:
  - Consider math or software problems
   - Some algorithms can give different results with the same dataset based on their nature (deterministic or stochastic) 
   - Different Software version can fetch different results leading to potential impacts on decision making
  - Consider real-world risks: who, what, when and how?
   - If the data does not have a proportionate participation of all ethnicities, it may result in disparity (group or individual fairness)
   - The Model does not account for unexpected changes caused by Economic Fallout due to Global Pandemic, Ukraine conflict etc.
    
- Describe potential uncertainties relating to the impacts of using your group's best remediated model:
  - Consider math or software problems
   - Data security is uncertain, breaches can directly impact lot of people
  - Consider real-world risks: who, what, when and how?
   - Using race/gender in the data can lead to ethnic or gender based profiling, which can impair decision making.
   - Bias in data can be augmented over time if the model trains itself on the same data.
   - Taking decisions based on data requires the data to be regularly scrutinised for biases. This demands transpareny which is beneficial to eliminate biases but can invite attacks/data poisoning incidents 
- Describe any unexpected or results encountered during training
  - black-to-white AIR: 0.74 which is lesser than expected 0.80
  - asian-to white AIR: 1.196 which is greater than expected (approaching the upper limit of 1.20)
  - female-to-male AIR: 0.957 which is close to the 1.00 AIR
