# Employee_Attrition_Hackathon
DataScience Project on Predicting Employee Attrition - AV Hackathon

# Problem Statement
You are working as a data scientist with HR Department of a large insurance company focused on sales team attrition. Insurance sales teams help insurance companies generate new business by contacting potential customers and selling one or more types of insurance. The department generally sees high attrition and thus staffing becomes a crucial aspect.

To aid staffing, you are provided with the monthly information for a segment of employees for 2016 and 2017 and tasked to predict whether a current employee will be leaving the organization in the upcoming two quarters (01 Jan 2018 - 01 July 2018) or not, given:

Demographics of the employee (city, age, gender etc.) Tenure information (joining date, Last Date) Historical data regarding the performance of the employee (Quarterly rating, Monthly business acquired, designation, salary)


# Approach
The data contains the information about the employees and their behaviors. The task in hand is to use ML to be able to predict and retain employee as losing employees frequently impacts the morale of the organization and hiring new employees is more expensive than retaining existing ones. 

The target variable is not directly mentioned in the train data, but by looking at the variables and with some commmon sense plus domain knowledge, we can easily determine that the ‘LastWorkingDate’ is the target column. If the column has some positive dates then the employee has left the cmpany otherwise still working with the same company. Hence, we can ecndoe this 0 and 1 {0: current employee, 1: ex-employee}.

The test data contains only the employee ids. Thus, to test the model on the test data we pull all the information for those employee id's from the train data.

After that I have applied some data preprocessing techniques such as grouping, encoding etc. and feature engineering such as creating tenure, daya on current role, etc. and try several supervised machine learning models. Whichever model gives the best accuracy as per the data we are feeding in the model, I have used that for predicting our test data.


# Data Preprocessing Steps
1) Convert to datetime and parse day, month, year, and yymm from the user_created_date
2) LastWorkingDate fillna for missing values
3) Create Target variable - 'Attrition {0: current employee, 1: ex-employee}'
4) Data Aggregation: There are multiple records for many employee id as they have changed the role or got promotions, etc. Therefore, we group the data on 'Emp_ID','Gender','Education_Level','City','Attrition'.
  4.1) We kept the last values for the following variables: 'Age','Salary','Joining Designation','Dateofjoining','Quarterly Rating','LastWorkingDate'
  4.2) We took the group sum of 'Total Business Value', 'Attrition'
  4.3) Concatenating both these groups to get a new dataframe
5) Calculating Tenure (number of months since resignation)
6) Calcuating Days on Current Role
7) Encode variables and dropping the original categorical variable which were encoded
8) I apply SMOTE technique as well becauase of the imbalanced target variable distribution


# Deciding The Final Machine Learning Model
After all the data preprocessing steps, many classification models have been tried and tested after splitting the data into train and test. However, final submission code here contains only final model which has been decided as per the local accuracy and public leaderboard score.

Here, I have chosen the GradientBoost model and went ahead for the final prediction. Hyperparameters has been tuned as well. F1 score was 0.81.
