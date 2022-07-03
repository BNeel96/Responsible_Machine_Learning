# Responsible_Machine_Learning
Content

Intended use

Primary intended uses:
** To predict whether or not the annual percentage rate (APR) charged for a mortgage is 150 basis points (1.5%) or more above a survey-based estimate of similar mortgages. (High-priced mortgages are legal, but somewhat punitive to borrowers. High-priced mortgages often fall on the shoulders of minority home owners, and are one of many issues that perpetuates a massive disparity in overall wealth between different demographic groups in the US.)
** The intended use is also to train an interpretable machine learning model, which is transparent and helps prevent biases.
Primary intended users: Students and academics interested in interpretable machine learning models.
Out-of-scope use cases: This is solely for educational purpose. Any use beyond an educational example is out-of-scope.
Describe the business value of your group's best remediated model

** The best remediated model is used for:
** Discrimination testing and attempt remediating of discovered discrimination using AIR (adverse impact ratio)
image
** Retrained the most accurate model above 0.8 AIR
** Best AUC: 0.7809 above 0.8 AIR (0.8116). Remediated EBM retrained with AUC: 0.7809.
** Checked that other groups are not adversely impacted y change: Adverse impact ratio for Asian people vs. White people: 1.146. Adverse impact ratio for Black people vs. White people: 0.812. Adverse impact ratio for Females vs. Males: 0.957 This analysis shows that even with a selective cutoff of 0.17, less discriminatory models are available. The new set of features and hyperparameters leads to a ~13% increase in AIR with a ~5% decrease in AUC.
Describe how your group's best remediated model is designed to be used

Describe the intended users for your group's best remediated model

State whether your group's best remediated model can or cannot be used for any additional purposes

Training data (2 pts.)

State the source of training data
** Home Mortgage Disclosure Act (HMDA) data in the class repository https://github.com/jphall663/GWU_rml/tree/master/assignments/data
State how training data was divided into training and validation data
** 70/30
State the number of rows in training and validation data
** Train data rows = 112253, columns = 23; and the Validation data rows = 48085, columns = 23
Define the meaning of all training data columns
Data dictionary:

|Name|Modeling| Role|	Measurement| Level|	Description|
-----|--------|-----|------------|------|------------|
high_priced	target	int	whether (1) or not (0) the annual percentage rate (APR) charged for a mortgage is 150 basis points (1.5%) or more above a survey-based estimate of similar mortgages
conforming	input	int	whether the mortgage conforms to normal standards (1), or whether the loan is different (0)
debt_to_income_ratio_std	input	int	standardized debt-to-income ratio for mortgage applicants
debt_to_income_ratio_missing	demographic information	int	missing marker (1) for debt to income ratio std
income_std	input	int	standardized income for mortgage applicants
**loan_amount_std **	input	int	standardized amount of the mortgage for applicants
**intro_rate_period_std **	input	int	standardized introductory rate period for mortgage applicants
loan_to_value_ratio_std	input	int	ratio of the mortgage size to the value of the property for mortgage applicants
no_intro_rate_period_std	input	int	whether (1) or not (0) a mortgage does not include an introductory rate period
property_value_std	input	int	value of the mortgaged property
term_360	input	int	whether the mortgage is a standard 360 month mortgage (1) or a different type of mortgage (0)
male	demographic information	int	whether a person identifies as male (1) or not male (0)
female	demographic information	int	whether a person identifies as female (1) or not female (0)
black	demographic information	int	whether a person identifies as black (1) or not black (0)
asian	demographic information	int	whether a person identifies as asian (1) or not asian (0)
white	demographic information	int	whether a person identifies as white (1) or not white (0)
amind	demographic information	int	whether a person identifies as amind (1) or not amind (0)
hipac	demographic information	int	whether a person identifies as hipac (1) or not hipac (0)
hispanic	demographic information	int	whether a person identifies as hispanic (1) or not hispanic (0)
non_hispanic	demographic information	int	whether a person identifies as non_hispanic (1) or not non_hispanic (0)
agegte62	demographic information	int	whether a person is over the age of 62 (1) or not over the age of 62 (0)
agelt62E	demographic information	int	whether a person is below the age of 62 (1) or not below the age of 62 (0)
row_id	ID	int	unique row indentifier
Define the meaning of all engineered columns
** phat and r were engineered for residual analysis.
** phat: It is a numeric input that helps to predict probabilities of high-priced mortgage
** r: It is a numeric input and is log loss residual for the predicted probabilities.
Evaluation data (2 pts.)
State the source of evaluation (or test) data
** Home Mortgage Disclosure Act (HMDA) data in the class repository https://github.com/jphall663/GWU_rml/tree/master/assignments/data
State the number of rows in evaluation (or test) data
** 19830 (without the header). With header it is 19831
State any di�erences in columns between training and evaluation (or test) data
** There is no difference in the columns between training and evaluation (or test) data with one exception. The high_priced column which is the target variable does not exist in test data.
Model details (2 pts.)
State the columns used as inputs in your group's best remediated model
** 'property_value_std', 'no_intro_rate_period_std', 'loan_amount_std', 'income_std', 'conforming', 'intro_rate_period_std', 'debt_to_income_ratio_std', and 'term_360'
State the columns used as targets in your group's best remediated model
** 'high_priced'
State the type of your group's best remediated model
** XGBoost
State the software used to implement your group's best remediated model
** 'xgboost', 'H20', 'interpret.glassbox', 'interpret.perf', 'numpy', 'pandas', 'time', 'matplotlib.pyplot', and 'matplotlib.lines'.
State the version of the modeling software for your group's best remediated model
** 'xgboost 1.4.2', 'h20 3.36.1.2', 'interpret 0.2.7', 'numpy 1.11.1', and 'pandas 0.19.2
State the hyperparameters or other settings of your group's best remediated model
** 'colsample_bytree': 0.3, 'colsample_bylevel': 0.9, 'eta': 0.05, 'max_depth': 5, 'reg_alpha': 0.005, 'reg_lambda': 0.0005, 'subsample': 0.7, 'min_child_weight': 5, 'gamma': 0.2, 'booster': 'gbtree', 'eval_metric': 'auc', 'monotone_constraints': (1, 1, 1, -1, 1, 1, -1, -1, -1, 1), 'nthread': 4, 'objective': 'binary:logistic', 'seed': 12345
Quantitative analysis (3 pts.)
State the metrics used to evaluate your group's best remediated model

** AUC
State the values of the metrics for training, validation, and evaluation (or test) data evaluation (or test) metrics come from the most recent class full evaluation results, link under Assignment 1.

** Explainable Boosting Machine - Validation AUC 0.8249 (RANK 1); Monotonic XGBoost - Validation AUC 0.7920 (RANK 2); and Elastic Net - Validation AUC 0.7538 (RANK 3)
Provide at least one plot or table from each weekly assignment for a total of at least six plots, that must include the global variable importance and partial dependence of your group's best remediated model.

** Assignment 1
image

** Assignment 2 (1st graph)
image

** Assignment 2 (2nd graph)
image

** Assignment 2 (3rd graph)
image

** Assignment 3
image

** Assignment 4 (1st graph)
image

** Assignment 4 (2nd graph)
image

** Assignment 5
Address other alternative models considered

Ethical considerations (2 pts.)
Describe potential negative impacts of using your group's best remediated model:
Consider math or software problems
Consider real-world risks: who, what, when and how?
** The model can improve accuracy but if there is bias in the data collection then it would lead to conflicting results.
** The model will become less useful if the economic conditions change dramatically. For example, if the model is built using pre-pandemic time period data, it would become less useful if we are trying to use the model during the pandemic.
Describe potential uncertainties relating to the impacts of using your group's best remediated model:
Consider math or software problems
Consider real-world risks: who, what, when and how?
Describe any unexpected or results encountered during training
