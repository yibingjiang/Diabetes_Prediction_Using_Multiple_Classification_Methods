# Diabetes prediction

## Background

Diabetes mellitus is a prevalent chronic disease that significantly impacts global health. It arises when the pancreas cannot produce enough insulin, or the body cannot effectively use it. This results in elevated glucose levels in the blood, which can lead to long-term damage to various organs and tissues. Early detection and management of diabetes are crucial for preventing these severe outcomes.

Machine learning (ML) in healthcare has shown promising results in enhancing diagnostic accuracy, personalizing treatment and improving patient outcomes. Specifically, ML techniques have been widely used to predict diabetes efficiently. Historical data from academic studies reveal that machine learning models can analyze complex datasets and identify patterns that might not be evident to human observers. For instance, researchers have employed algorithms like logistic regression, support vector machines, and neural networks to predict diabetes onset with high accuracy based on risk factors such as age, weight, and genetic history (Kavakiotis et al., 2017; Maniruzzaman et al., 2018).

This project builds on the foundation of these previous works, aiming to leverage demographic and health-related data to predict the likelihood of diabetes using sophisticated machine-learning techniques. By integrating diverse features, such as BMI, blood glucose levels, and hypertension status, this project seeks to provide a comprehensive analysis that could aid in early diagnosis and better diabetes management.

## Data Description

The dataset consists of 100,000 individuals and includes demographic, health, and lifestyle features:

| Feature             | Description |
|---------------------|-------------|
| **gender**          | Gender refers to the biological sex of the individual, which can impact their susceptibility to diabetes. Categories include male, female, and other. |
| **age**             | Age is a significant factor as diabetes is more commonly diagnosed in older adults. Age ranges from 0 to 80 years in our dataset. |
| **hypertension**    | Hypertension is a condition where blood pressure in the arteries is persistently elevated. It is coded as 0 (no hypertension) or 1 (has hypertension). |
| **heart_disease**   | Heart disease is linked with an increased risk of developing diabetes. It is coded as 0 (no heart disease) or 1 (has heart disease). |
| **smoking_history** | Smoking history is considered a risk factor for diabetes. Categories in our dataset include not current, former, no info, current, never, and ever. |
| **bmi**             | Body Mass Index (BMI) is a measure of body fat based on weight and height. The range in our dataset is from 10.16 to 71.55. Categories are underweight (<18.5), normal (18.5-24.9), overweight (25-29.9), and obese (≥30). |
| **HbA1c_level**     | Hemoglobin A1c level measures average blood glucose over 2-3 months. Higher levels (>6.5%) indicate a greater risk of diabetes. |
| **blood_glucose_level** | Blood glucose level measures the amount of glucose in the blood at a given time. High levels are a primary indicator of diabetes. |
| **diabetes**        | Diabetes is the target variable, with 1 indicating the presence of diabetes and 0 indicating its absence. |

## EDA

### Distribution of Diabetes

The bar plot illustrating the distribution of diabetes within the dataset highlights a significant class imbalance. Non-diabetic individuals constitute 91.5% of the dataset, while only 8.5% are marked as diabetic. This imbalance is a critical consideration for model training as it can influence the predictive performance, possibly leading to a model biased towards predicting the majority class. In the later part, we will use k-fold cross-validation to handle this problem.

![diabetes_distribution](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/b399bdf1-f67c-4a7f-b997-5b9603cba5d1)

### Correlation Analysis

A correlation plot among numeric variables and binary factors revealed some expected associations, such as between age, BMI, blood glucose levels, and HbA1c levels with diabetes status. These relationships are intuitive, as higher values of BMI, blood glucose, and HbA1c are commonly associated with increased risks of diabetes.

![correlation matrix](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/ea1fe6ca-272a-4f7b-b296-416925897527)

### Age and BMI

![age-bmi](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/3d79e626-b780-4392-b8d0-aba1ff2cdc0e)

**Age**: The median age of diabetic individuals is higher than that of non-diabetics. This suggests that age is a significant risk factor and should be weighted appropriately in the predictive model.

**BMI**: Higher BMI values in diabetic individuals underscore the well-established link between obesity and type 2 diabetes. The wide range of BMI values among diabetics—from underweight to obese—suggests that while higher BMI is a risk factor, other variables must also play significant roles in diabetes development.

### Blood Glucose and HbA1c Levels

![Blood Glucose and HbA1c Levels](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/3469f238-9c8a-4b01-a8bb-4a8b78e56222)

**Blood Glucose Levels**: Diabetic individuals typically show higher fasting blood glucose levels, which directly relate to diabetes diagnosis criteria.

**HbA1c Levels**: HbA1c levels greater than 6.5% are diagnostic for diabetes, and the boxplots clearly separate diabetic from non-diabetic individuals based on this criterion.

### Gender

![gender](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/25d48fcc-0f47-439f-994e-b0c2c87949ea)

The grouped bar plot by gender shows a slightly higher proportion of diabetic cases in males than females, suggesting a gender-specific prevalence that could be explored further. Also, there are fewer observations with the "Other" gender, which will cause an imbalance problem for our later model construction. Therefore, we will handle this problem in the data processing part.

### Smoking History

![smoking](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/581aeddd-0cb1-4204-a771-a88d88c5e8ae)

**Former Smokers**: The proportion of former smokers is notably higher in the diabetic group. This could indicate that individuals who have quit smoking still retain a residual increased risk of developing diabetes, possibly due to lasting physiological changes or cumulative effects from their smoking years.

**Current Smokers**: Similarly, current smokers are more prevalent among diabetics than non-diabetics. This aligns with existing research that links smoking to insulin resistance and inflammation, contributing factors to the development of diabetes.

**Never Smokers**: This category, while still significant, comprises a smaller percentage of the diabetic group compared to the non-diabetic group, reinforcing the notion that smoking may elevate diabetes risk.

## Model Setup and Evaluation

### Model Building

Four models were considered:
**1) Logistic Regression**, **2) Linear Discriminant Analysis (LDA)**, **3) Naive Bayes**, and **4) Random Forest**. Each model was evaluated using a 10-fold cross-validation approach to ensure the robustness and generalizability of the predictions.

### Model Performance:
The performance of each model was assessed using several metrics, including recall, precision, F-measure, accuracy, kappa, ROC AUC, sensitivity, and specificity. The ROC curves plotted for each model indicate their effectiveness in distinguishing between the diabetic and non-diabetic classes.

#### Logistic Regression

![log-reg_roc](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/e0a5eb3b-6437-4633-84a7-edfbc368142d)

#### LDA

![LDA_roc](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/e22488ee-3872-4411-a36f-92ad926a7d25)

#### Naive Bayes 

![nb_roc](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/5f37dafa-bdad-420b-96c8-b077514c3bb8)

#### Random Forest

![rf_roc](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/6219ac98-5184-42c6-870e-a5a05ac45e67)

## Model Selection

We then draw a bar plot to compare the ROC scores of four models and identify the best one.

![model_comparison](https://github.com/yibingjiang/Diabetes_prediction/assets/141768352/b3e7c33b-cd42-46d8-b973-2d8cf64582d3)

Based on the plot, Random Forest performs best, with a 0.97 ROC score, followed by log regression and LDA, which have 0.96 and 0.95, respectively.  

## Discussion

The exploration and modeling of the dataset in this project have unearthed several critical insights into the predictive modeling of diabetes using demographic and health-related variables. Applying various machine learning models—Logistic Regression, Linear Discriminant Analysis, Naive Bayes, and Random Forest—has each demonstrated unique strengths in handling predictions. Logistic Regression and Random Forest were particularly effective, likely due to their robustness and ability to model complex, non-linear relationships among the data features. These models showed promising performance, especially in handling the imbalanced nature of the dataset, with Random Forest slightly edging out in performance in terms of ROC AUC metrics.

Despite these advancements, the project was not without limitations. The significant imbalance in the dataset, particularly with a larger number of non-diabetics, might have influenced the generalizability of the models. Additionally, substantial missing data in lifestyle-related variables like smoking history could have introduced biases, potentially weakening the models' capability to capture all relevant predictors effectively. Furthermore, the complexity of models like Random Forest raises concerns about overfitting, which could limit their practical application without rigorous external validation.

## Conclusion

This project marks a successful endeavor in applying machine learning techniques to predict diabetes using demographic and health-related data. It validated the importance of several medical indicators and highlighted the potential link between lifestyle factors such as smoking and the risk of diabetes. These findings could guide future preventive strategies and interventions.

Enhancing the dataset by focusing on underrepresented groups and expanding data on lifestyle factors could improve model accuracy and robustness. Additionally, experimenting with more sophisticated or newer algorithms might uncover better-performing or more interpretable models. The ultimate test, however, would be deploying these models in a clinical setting for real-time prediction and closely monitoring their performance over time. This practical application would provide invaluable feedback that could be used to refine the models, making them more suitable for widespread use in healthcare settings.
