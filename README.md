## Heritage House Sales Price Prediction

This project aims to understand and predict house prices by analyzing various factors that contribute to the sale price. We explore the relationships between house attributes and sale prices using statistical techniques like correlation analysis. Through this investigation, we aim to validate specific hypotheses and uncover key drivers that influence house prices in Ames, Iowa.

![Multi Device Mockup](docs/readmescreenshots/techsini_screenshot_pp5.png)

The project is deployed here: **[Deployed Project](https://ameshouseproject-2e20e722aa63.herokuapp.com/)**

The project's repository can be accessed here: **[GitHub Repository](https://github.com/Werner-Staeblein/Project-5)**

# Table of Contents
- [Table of Contents](#table-of-contents)
  - [1. Dataset Content](#1-dataset-content)
  - [Project Terms used | Jargon explained](#project-terms-used--jargon-explained)
  - [2. Business Requirements](#2-business-requirements)
    - [EPICS](#epics)
    - [User Stories (US)](#user-stories-us)
  - [3. Hypothesis and how to validate hypothesis](#3-hypothesis-and-how-to-validate-hypothesis)
  - [4. Rationale to map the business requirements to the Data Visualisations and ML tasks](#4-rationale-to-map-the-business-requirements-to-the-data-visualisations-and-ml-tasks)
  - [5. ML Business Case](#5-ml-business-case)
  - [7. **CRISP-DM**](#7-crisp-dm)
  - [| 6. Deployment | move the application into production to allow users to take advantage of it |](#-6-deployment--move-the-application-into-production-to-allow-users-to-take-advantage-of-it-)
  - [7. Data Preprocessing](#7-data-preprocessing)
    - [Data Cleaning Pipeline](#data-cleaning-pipeline)
    - [Feature Engineering](#feature-engineering)
      - [Categorical encoding](#categorical-encoding)
      - [Numerical Transformation](#numerical-transformation)
  - [8. Dashboard Design](#8-dashboard-design)
  - [Page 1: Quick Project Summary | Opening Page of the Dashboard](#page-1-quick-project-summary--opening-page-of-the-dashboard)
  - [Page 2: Correlation Page](#page-2-correlation-page)
      - [Target Analysis](#target-analysis)
  - [Page 3: House Price Predictor Page](#page-3-house-price-predictor-page)
  - [Page 4: Hypothesis](#page-4-hypothesis)
  - [Page 5: Technical Page | Model Performance Page](#page-5-technical-page--model-performance-page)
    - [R2 Explanation](#r2-explanation)
    - [Performance Evaluation](#performance-evaluation)
  - [9. Fixed Bugs | Deployment challenges](#9-fixed-bugs--deployment-challenges)
    - [Seeking advice](#seeking-advice)
    - [What was the key reason for the bug(s)?](#what-was-the-key-reason-for-the-bugs)
    - [Lessons Learned](#lessons-learned)
  - [10. Manual Testing](#10-manual-testing)
    - [Widget input testing](#widget-input-testing)
    - [Sanity Check on Regression Model](#sanity-check-on-regression-model)
  - [11. Deployment](#11-deployment)
    - [Heroku](#heroku)
  - [12. Packages and technologies used](#12-packages-and-technologies-used)
    - [Technologies used:](#technologies-used)
    - [Main Data Analysis and Machine Learning Libraries](#main-data-analysis-and-machine-learning-libraries)
  - [Credits](#credits)
    - [Code](#code)
    - [Media](#media)
    - [**Content**](#content)
  - [Acknowledgements](#acknowledgements)

## 1. Dataset Content

* The dataset is sourced from **[Kaggle](https://www.kaggle.com/codeinstitute/housing-prices-data)**. Fictitious user stories were created where predictive analytics can be applied in a real project in the workplace.
* The dataset has almost 1.5 thousand rows and represents housing records from Ames, Iowa, indicating house profile (Floor Area, Basement, Garage, Kitchen, Lot, Porch, Wood Deck, Year Built) and its respective sale price for houses built between 1872 and 2010.

|Variable|Meaning|Units|
|:----|:----|:----|
|1stFlrSF|First Floor square feet|334 - 4692|
|2ndFlrSF|Second-floor square feet|0 - 2065|
|BedroomAbvGr|Bedrooms above grade (does NOT include basement bedrooms)|0 - 8|
|BsmtExposure|Refers to walkout or garden level walls|Gd: Good Exposure; Av: Average Exposure; Mn: Minimum Exposure; No: No Exposure; None: No Basement|
|BsmtFinType1|Rating of basement finished area|GLQ: Good Living Quarters; ALQ: Average Living Quarters; BLQ: Below Average Living Quarters; Rec: Average Rec Room; LwQ: Low Quality; Unf: Unfinshed; None: No Basement|
|BsmtFinSF1|Type 1 finished square feet|0 - 5644|
|BsmtUnfSF|Unfinished square feet of basement area|0 - 2336|
|TotalBsmtSF|Total square feet of basement area|0 - 6110|
|GarageArea|Size of garage in square feet|0 - 1418|
|GarageFinish|Interior finish of the garage|Fin: Finished; RFn: Rough Finished; Unf: Unfinished; None: No Garage|
|GarageYrBlt|Year garage was built|1900 - 2010|
|GrLivArea|Above grade (ground) living area square feet|334 - 5642|
|KitchenQual|Kitchen quality|Ex: Excellent; Gd: Good; TA: Typical/Average; Fa: Fair; Po: Poor|
|LotArea| Lot size in square feet|1300 - 215245|
|LotFrontage| Linear feet of street connected to property|21 - 313|
|MasVnrArea|Masonry veneer area in square feet|0 - 1600|
|EnclosedPorch|Enclosed porch area in square feet|0 - 286|
|OpenPorchSF|Open porch area in square feet|0 - 547|
|OverallCond|Rates the overall condition of the house|10: Very Excellent; 9: Excellent; 8: Very Good; 7: Good; 6: Above Average; 5: Average; 4: Below Average; 3: Fair; 2: Poor; 1: Very Poor|
|OverallQual|Rates the overall material and finish of the house|10: Very Excellent; 9: Excellent; 8: Very Good; 7: Good; 6: Above Average; 5: Average; 4: Below Average; 3: Fair; 2: Poor; 1: Very Poor|
|WoodDeckSF|Wood deck area in square feet|0 - 736|
|YearBuilt|Original construction date|1872 - 2010|
|YearRemodAdd|Remodel date (same as construction date if no remodelling or additions)|1950 - 2010|
|SalePrice|Sale Price|34900 - 755000|

## Project Terms used | Jargon explained

* **Sale price** is the market price of a house with features represented by the list of features for the respective house. 
* **inherited house** is a house that the client inherited from grandparents that needs evaluation of market price
* **summed price** is total sum of all predicted market prices of all four houses that the client inherited

## 2. Business Requirements

Our client has received an inheritance from a deceased great-grandfather. Included in the inheritance are four houses located in Ames, Iowa, USA. 
Although the client has an excellent understanding of property prices in her home country, she fears that basing her estimates for property worth on 
her current knowledge of the Iowan market might lead to inaccurate appraisals. What makes a house desirable and valuable where she comes from might 
not be the same in Ames, Iowa.

Our client has provided us a public dataset with house prices for Ames, Iowa. Our client has asked us to help to maximize the sale price for
the inherited properties with predictions on the sale price to be made for the four houses inherited based on the respective attributes of those
houses.

The business requirements are:												
                                                
* **BR1** - The client is interested in discovering how the house attributes correlate with the sale price in the Ames, Iowa, region. Therefore, the client expects **data visualisations** of the **correlated variables** against the sale price to show that.

* **BR2** - The client is interested in predicting the house sale price from her four inherited houses, and any other house in Ames, Iowa.

To address the business requirements, Epics and User Stories were defined. The user stories are broken down into small tasks so that an agile process can be used to implement each task/user story.

### EPICS

* Data collection and information gathering

* Visualisation of data, data cleaning and data preparation

* Train the model, optimize the model and validate the model

* Plan the dashboard, design and develop the dashboard

* Dashboard deployment on Heroku and release

### User Stories (US)

The user stories are defined by the business requirements.

* **User Story 1**: The client wants to know those attributes of a house that are most correlated with its potential sale price. The prediciton of a sale price shall be based on the set of features with the highest predictive power.
Business requirement addressed: BR 1

* **User Story 2**: The client wants to have a the best possible prediction of the sales price of the houses inherited. The client wants to achieve the maximum possible proceeds for the four houses inherited.
Business requirement addressed: BR 2

* **User Story 3**: As a developer I can **install all requirements and packages** so that I can **work with the tools needed to complete the task**
Business requirement addressed: BR 1 & 2

* **User Story 4**: As a developer I can **start the deyployment process of my app on Heroku early** so that **I have a possibility for end-to-end manual deployment testing from the beginning**
Business requirement addressed: BR 1 & 2

* **User Story 5**: As a developer I can **import relevant data into Jupyter Notebook** so that **I can analyze the dataset**
Business requirement addressed: BR 1 & 2 

* **User Story 6**: As a developer I want **a dependable cleaning process** so that I can **ensure that the dataset collected is accurate and of high quality**
Business requirement addressed: BR 1

* **User Story 7**: As a developer I want **to measure the model performance** so that I **can have reliable results with high predictive power**
Business requirement addressed: BR 1 & 2

* **User Story 8**: As a developer I can **create a dashboard** so that I **can display the results of model predictions**
Business requirement addressed: BR 2

* **User Story 9**: As a User **I can see the Streamlit starting page** so that **I can quickly see the overview over the project**      
Business requirement addressed: BR 2

* **User Story 10**: As a User, I want **to see a correlation page on Streamlit** so that I **can understand the correlation of features with the target variable**                 
Business requirement addressed: BR 2

* **User Story 11**: As a User I want to **test individual observations against the model outcome** so that I **can determine the target variable with my features provided**
Business requirement addressed: BR 2

* **User Story 12**: As a User I want to **have interactive input fields** so that I **can provide individual data to predict the target variable**	
Business requirement addressed: BR 2

* **User Story 13**: As a User I want to **see data plots with visualizations for the relationship between the target variable and the features**
Business requirement addressed: BR 2

## 3. Hypothesis and how to validate hypothesis

We propose the following hypotheses to explain the relationship between house attributes and sale price:

1.	Size Hypothesis:
Larger properties tend to have higher absolute sale prices. 

- We will investigate correlations between attributes related to house size (e.g., square footage, number of bedrooms) and sale price to validate this hypothesis.

2.	Overall Quality Hypothesis:
We suspect that the overall quality of a house will significantly impact the sale price. The higher the quality rating, the higher the expected sale/market price.

- We will investigate correlations between attributes related to the quality assessment of the house such as 'OverallQual' or 'KitchenQual' to validate the hypothesis

3.	Overall Condition Hypothesis:
We suspect that the overall condition of a house will influence the sale price. Houses in better condition should command a higher price.

- We will investigate the data on the 'YearBuilt' or 'YearRemodAdd' to validate this hypothesis.

## 4. Rationale to map the business requirements to the Data Visualisations and ML tasks

* List your business requirements and a rationale to map them to the Data Visualisations and ML tasks.
                                               
* **Business Requirement No. 1**: Visualisation of Data and Correlation Study 
  
  - Correlation Study (Pearson and Spearman) to verify how house attributes/variables are correlated with the target
  - Determine the significance of correlation
  - The variables of the dataset representing the attributes of houses in the dataset are plotted against the house price to gain insight into correlation
  - The business requirement is addressed in this notebook: **[Correlation Study](jupyter_notebooks\03_correlation_study.ipynb)**
 
* **Business Requirement No. 2**: Regression Analysis

- The target variable (house price) is continuous. Therefore, a regression analysis is conducted to address the business requirement. If a regression model proves to perform poorly on required metrics, a classification analysis can be done
- The business requirement is addressed in this notebook: **[ML Modeling](jupyter_notebooks\05_ml_model_and_evaluation.ipynb)**
- The ML task will be to forecast house sale prices based on attributes of houses provided. The ML task is achieved by using the key features determined such as OverallQual, GrLivArea or GarageArea

## 5. ML Business Case

* Frame the business case using the method we covered in the course.

- Business requirements

    - The client wants to know how house attributes correlate with sale price. The client expects data visualisations of correlated features with the sale price
    - The client wants to predict house sales prices for the 4 inherited houses. In addition, the client want to prdict house sale price for other houses in Ames, Iowa

- Can traditional data analysis be used

    - The client could approximate the sale prices of houses inherited by drawing inferences from the datapoints in the dataset for houses with similar features. This approach may, however, lead to inaccuracies and is very subjective

- Does the customer need a dashboard or API

    - The client needs a dashboard
  
- A successful project outcome for the client is defined as

    - an analysis that shows the variables most correlated with the sale price to help the client to *maximize the sale price* for houses inherited

- Are there any ethical or privacy concerns

    - The dataset is public. Therefore, there are no ethical or privacy concerns

- Are there clear EPICS and user stories for agile implementation

    - EPICS were defined., User stories were created and organized as GitHub issues on a Kanban board in GitHub, enabling clear tracking for agile implementation.
    - The GitHub project board can be found here: **[GitHub Project Board](https://github.com/users/Werner-Staeblein/projects/27)**
    - EPICS are broken down as follows

      - Information gathering and data collection,
      - Data visualization, cleaning, and preparation,
      - Model training, optimization and validation,
      - Dashboard planning, designing, and development,
      - Dashboard deployment and release.

- Does the data suggest a particular model

    - For a continuous numeric prediction target, a regression model is appropriate
  
- What are the project inputs and intended outputs

    (a) Model inputs are house attributes from the public dataset

    (b) Output is the predicted sales price in USD, a continuous numeric value

    The model should predict sale price of a house based on the known attributes of the house inherited

     - The client has provided the *attributes* of the houses inherited. For each of the 4 houses, the model shall predict sale price based on these *known attributes*. An additional output is the sum of the predicted sale price for all four inherited houses combined
  
     - A user of the dashboard shall be enabled to predict house price for any house that is not any of the four houses inherited by the client. The user can enter *attributes* for a given hosue through input widgets and receives live data for the estimated sale price

- What does succes look like

    - It was agreed with client that a R2 score of at least 0.75 on the train set and test set is defined as success
    
- How will the client benefit

    - The client will maximize the sales price for the inherited properties using a reliable model to determine the sale price for each house inherited


## 7. **CRISP-DM**
This project uses the CRISP-DM ("CRoss Industry Standard Process for Data Mining") process model to develop the data science process.

| Process | Description |
| --- | --- |
| 1. Business Understanding: | understanding the objectives and requirements |
| 2. Data Understanding | gather data, analyze it and identify opportunities |
| 3. Data Preparation | prepare the data with the appropriate cleaning and engineering for modelling |
| 4. Modelling | research and identify the structure of the model and build it |
| 5. Evaluation | identify the best performing solution and assess if it meets the desired requirements |
| 6. Deployment | move the application into production to allow users to take advantage of it |
---


## 7. Data Preprocessing

### Data Cleaning Pipeline

A data cleaining pipeline was prepared to address missing values. 

Continuous Variables such as ['LotFrontage'] and ['BedroomAbvGr'] with missing values have been imputed with the mean as there were
no large outliers and to keep the imputed values with the range of observed values in the dataset.

Continuous Variables with skewness in the data such as ['2ndFlrSF'] and ['MasVnrAreaand'] with missing values have been imputed with the median. 
This reduces the influence of outlier data on the imputed values.

Categorical variables ['GarageFinish'], ['BsmtFinType1'], ['BsmtExposure'] likely have missing values because the respective feature is
not applicable/observable/existent for the respective property. These values are filled/imputed with 'None' so that the observation that
any such respective feature may not exist remains captured in the dataset. The fact that something "does not exist" remains an informative
datapoint for the remainder of the analysis.

Features ['EnclosedPorch'], ['GarageYrBlt'], ['WoodDeckSF'] with missing data were removed from the dataset. This is mainly because two
of these features have a substantial number of missing values. Imputing from a low number of observations (10%) to a much larger number
of missing observations (around 90%) lkely distorts the dataset. In addition, the features dropped likely do not have a high predictive
power for the target as defined in the analtiyical hypothesis.

Further explanations on the analytical rationale to address the missing data in the dataset can be found in the file **[Data Cleaning](jupyter_notebooks\02_data_cleaning.ipynb)**
 
### Feature Engineering

#### Categorical encoding

Categorical encoding was used to convert ordinal categories into numerical values. This keeps the order of the categories and the relative hierarchy
was included in the regression analysis. Most of the ordinal categories, however, were dropped in the data cleaning process.

#### Numerical Transformation

| **Feature**      | **Evaluation**                                                                                   | **Transformation used**                                                                                       |
|-------------------|----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| TotalBsmtSF       | The mean imputation method was most effective for handling missing values.                  | MeanMedianImputer                                                            |
| GrLivArea         | Applying logarithmic transformation was most effective to normalize | LogTransformer.                                                                                               |
| TotalBsmtSF       | Power transformation was most effective to normalize | PowerTransformer.                                                                                             |
| TotalBsmtSF, GarageArea | Winsorizing with the IQR method was most effective to handle outliers | Winsorizer                                         |
| TotalBsmtSF, GrLivArea, GarageArea | Standard scaling was most effective to normalize feature ranges | StandardScaler.                                                                                              |

## 8. Dashboard Design

## Page 1: Quick Project Summary | Opening Page of the Dashboard

This page shows a summary of
 
<details>
<summary> Key terms and jargon used in the project</summary>

* **Sale price** is the market price of a house with features represented by the list of features for the respective house. 
* **inherited house** is a house that the client inherited from grandparents that needs evaluation of market price
* **summed price** is total sum of all predicted market prices of all four houses that the client inherited
</details>
 
<details>
<summary> The project dataset</summary>

* The project is based on a dataset of housing prices from Ames, Iowa.
* The dataset is sourced from [Kaggle](https://www.kaggle.com/codeinstitute/housing-prices-data).
* The dataset includes sales price (the target to be predicted) and features for each house such as age (year built, year remodeled), size (first floor area, second floor area, garaze area) and quality
</details>
 
<details>
<summary> The business requirements</summary>

The project has 2 business requirements:

* **BR1** - The client is interested in discovering how the house attributes correlate with the sale price in the Ames, Iowa, region. Therefore, the client expects **data visualisations** of the **correlated variables** against the sale price to show that.

* **BR2** - The client is interested in predicting the house sale price from her four inherited houses, and any other house in Ames, Iowa.
</details>

<details>
<summary>Page 1: Project Overview (Screenshot)</summary>

<img src="docs/readmescreenshots/project_overview_page.png">
</details>

## Page 2: Correlation Page

![Screenshot Correlation Page](docs/readmescreenshots/screenshot_correlation_page_pp5.png)

This page shows

* the business requirement that was handled by the BR1 (correlation study)
* a checkbox that displays the dataset ("Inspect house data from the area")
* analytical conclusions about the features that have strongest correlation with the target (house sale price)

* a checkbox for displaying plots of sale price and each of the features that have strong correlation. This section of the page displays:
  * the distribution of the target variable (sale price)
  * regression plots of sale price and each of the continuous numerical features
  * box plots of sale price and each of the categorical features
  * line graphs of sale price and each of the time variables
  * heatmaps showing correlations

<details>
<summary>Pearson Correlation Heatmap</summary>
<img src="docs/plots/heatmap_corr_pearson.png">
</details>

<details>
<summary>Spearman Correlation Heatmap</summary>
<img src="docs/plots/heatmap_corr_spearman.png">
</details>

<details>
<summary> PPS Heatmap</summary>
<img src="docs/plots/heatmap_pps.png">
</details>

#### Target Analysis

SalePrice is the target variable. The distribution of the target variable is studied with a histogram. 

![Histogram of SalePrice target variable](docs/plots/hist_plot_SalePrice.png)

The features most correlated with the target are analysed further. To analyse the relationships between
SalePrice and each (important) created different types of plots

- Features with continuous values displayed in a scatter plot
- Features with categorical values displayed in a box plot
- Features with time values displayed in a line plot

<details>
<summary>Click here to see the different plots</summary>
<img src="docs/plots/lm_plot_price_by_1stFlrSF.png">
<img src="docs/plots/lm_plot_price_by_GarageArea.png">
<img src="docs/plots/lm_plot_price_by_GarageYrBlt.png">
<img src="docs/plots/lm_plot_price_by_GrLivArea.png">
<img src="docs/plots/box_plot_price_by_KitchenQual.png">
<img src="docs/plots/box_plot_price_by_OverallQual.png">
<img src="docs/plots/lm_plot_price_by_TotalBsmtSF.png">
<img src="docs/plots/line_plot_price_by_YearBuilt.png">
<img src="docs/plots/line_plot_price_by_YearRemodAdd.png">
</details>



## Page 3: House Price Predictor Page

![Screenshot House Price Predictor Page](docs/readmescreenshots/screenshot_house_price_prediction.png)

- The page displays the four houses's attributes and their respective predicted sales price
- The sum of predicted sales prices for all four inherited houses is shown
- Interactive widgets to allow a user to provide real-time house data to predict the sale price on a any given house
- Manual testing was done on the widgets to verify that the feature order works correctly **[Widget Input Testing](#widget-input-testing)** 
- Sanity checks were done on the predictions of individual houses prices
**[Sanity Check on Regression Model](#sanity-check-on-regression-model)**

## Page 4: Hypothesis

![Screenshot Project Hypothesis and Validation](docs/readmescreenshots/project_hypothesis_and_validation_page.png)

First Hypothesis: **Size Hypothesis** 
We hypothesize that larger properties tend to have higher absolute sale prices.

Hypothesis confirmed: The correlation study shows that features that capture the size of a property 
such as '1stFlrSF', 'GarageArea', 'GrLivArea' 'TotalBsmtSF' have proven to be positively and moderately correlated with sale price.

Second Hypothesis: **Quality Hypothesis** 
We suspect that the overall quality of a house will significantly impact the sale price. The higher the quality rating, the higher the expected sale/market price.

Hypothesis confirmed: The correlation between sale price and features such as 'KitchenQual_TA' and 'OverallQual' showed that hypothesis cannot be proven wrong and is likely correct.

Third Hypothesis: **Overall Condition Hypothesis** 
We suspect that the overall condition of a house will influence the sale price. Houses in better condition should command a higher price.

Hypothesis confirmed: The hypothesis was validated with correlations between the sale price and features such as 'YearBuilt' or 'YearRemodAdd'. These features correlated positively and moderately with sale price.

## Page 5: Technical Page | Model Performance Page

![ML model dashboard page part 1](docs/readmescreenshots/machine_learning_model_screenshot_part1.png)

![ML model dashboard page part 1](docs/readmescreenshots/machine_learning_model_screenshot_part2.png)

The model performance page addresses business requirement No. 2. The dashboard page allows the client to predict the house sale price for her four inherited houses and any other house in Ames, Iowa.

### R2 Explanation
The R2 score measures the proportion of variance in the target variable explained by the model. A R2 score closer to 1 indicates high predictive power

### Performance Evaluation
- The agreed minimum R2 score of **0.75** was met for both the train (**0.88**) and test (**0.791**) sets, demonstrating strong model performance  
- The Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE) indicate that prediction errors are within an acceptable range. There are slightly higher error values on the test set compared to the train set

- The technical page describe the ML pipeline steps applied

## 9. Fixed Bugs | Deployment challenges

I had significant problems deploying the application. Locally on my computer, the Streamlit app worked well. However, deploying it on Heroku proved to be a major challenge. The history of the commit messages shows that I had to experiment extensively with different variations in the `requirements.txt` file to resolve package conflicts.

I did start PP-5 initially with deployment of the streamlit app. So, even before starting the pipeline and working on the machine learning model and underlying business requirements, I did inititate the project with deployment tests as I was fully aware and advised earlier that deployment could prove to be the bottleneck and issue. Unfortunately, the approach of starting off with deployment has not avoided completeley all the work necessary to run the streamlit app in heroku.

### Seeking advice
I exchanged information with the CI student support team on Slack: **[Slack exchange with student support](https://app.slack.com/client/T0L30B202/C02NH8VL28G)**

### What was the key reason for the bug(s)?
In my view, the deployment issues were primarily related to the fact that I had to update the machine learning model (Notebook 5) again using the locally installed version of `scikit-learn` and to ensure that `requirements.txt` includes exactly the packages I used to train the model. Debugging the deployment problems was extremely time-consuming and could only be resolved through trial and error.

### Lessons Learned
- While some information about Heroku error messages was readily available online, solving the deployment issues often required extensive notes and analysis.
- I focused on understanding which package versions in the `requirements.txt` file were incompatible with others and systematically addressed the conflicts.
- Despite the struggles on deployment, I will nevertheless continue to work on deployment at every start of every new project and continue with my personal habit of cross-checking deployment while working on a project.

## 10. Manual Testing

### Widget input testing

* The widget for OverallQual does not accept values less than 1 or greater than 10. Manual input within the range is accepted. Values outside the boundary result in a warning to the user.

* The values in widgets for continuous value features can be changed with the +/- sign in the widget, but can also be entered manually. Values for categorical features of ordinal nature (e.g., "OverallQual") can be entered manually or adjusted with the +/- sign in the widget.

* Verify the calculation with widgets to ensure proper functionality: Important features for house 1 (index 0) should be entered into the widgets to verify that the projected sales price matches US$ 130,229. The same steps should be repeated for houses 2 to 4 to verify that the widgets calculate the projected price based on regression analysis. This testing step ensures that calculations based on widget inputs are consistent with the regression analysis used to determine the individual house prices of the inherited properties.

### Sanity Check on Regression Model

I performed a manual sanity check on the regression model by comparing the predicted **SalePrice** with the known **SalePrice** in the dataset. This sanity check verifies that the model's calculations align with the underlying dataset.

This approach of "heuristically" cross-checking the regression outcomes helps ensure that model predictions and the assumptions made during the pipeline definition of the ML model are logical and consistent.

- **Manually comparing SalePrice values:** Cross-checked the predicted SalePrice with the actual SalePrice for several records in the dataset.
  
- **Feature validation:** Verified if the features determined to be of importance correlate logically with the SalePrice.

## 11. Deployment

### Heroku

The project was deployed to Heroku

* The App live link is: [**Heritage Housing Project**](https://ameshouseproject-2e20e722aa63.herokuapp.com/)

* Set the Python version to 3.9.12 in your runtime.txt. With this python version you can use the Heroku-24 stack.

Steps for deployment on Heroku are:

1. Log in to Heroku and create an App
2. At the Deploy tab, select GitHub as the deployment method.
3. Select your repository name and click Search. Once it is found, click Connect.
4. Select the branch you want to deploy, then click Deploy Branch.
5. The deployment process should happen smoothly if all deployment files are fully functional. Click the button Open App on the top of the page to access your App.
6. If the slug size is too large then add large files not required for the app to the .slugignore file. The code in this project has a sufficiently slug size for the application to be deployed with no problems.

## 12. Packages and technologies used
                                        
### Technologies used:

**[Git](https://git-scm.com/)** The version control system Git was used to document the development of the application and to push code to the GitHub repository. The specific reasons for the commit are reflected in the respective commit message

**[GitHub](https://github.com/)** The code files, README files, and assets are stored on GitHub. The code on GitHub was pushed from Git
                                                            
**[Heroku](https://www.heroku.com/)** Heroku is a platform as a service (PaaS) to build, run, and operate applications cloud-based. It was used to deploy the website

**[CI Python Linter](https://pep8ci.herokuapp.com/)** The Code Institute Python Linter was used to validate Python code			

**[Techsini](https://techsini.com/multi-mockup/)** Multi Device Website Mockup generator
           
**[Visual Studio Code](https://code.visualstudio.com/)** Visual Studio Code (VS-Code) was used as integrated development environment (IDE) for the entire project. The GitHub repository was cloned to VS-Code for this purpose	

### Main Data Analysis and Machine Learning Libraries											

The version number of the libraries used can be found in the **[requirements file](https://github.com/Werner-Staeblein/Project-5/blob/main/requirements.txt)** of this project

**[Feature Engine 1.0.2](https://feature-engine.trainindata.com/en/latest/)** Feature-engine is a Python library with multiple transformers to engineer and select features for machine learning models

**[Imbalanced-learn](https://pypi.org/project/imbalanced-learn/)** used to handle improve model performance in deployed machine learning projects.  

**[Joblib >=1.2.0](https://pypi.org/project/joblib/)** used for efficient serialization and deserialization of machine learning models and pipelines for deployment.

**[Jupiter Notebooks](https://jupyter.org/)** Open-source web app to create and share documents

**[Kaggle 1.6.12](https://pypi.org/project/kaggle/)** Tool for download of dataset from Kaggle
                                                     
**[Matplotlib 3.3.1](https://matplotlib.org/)** Data visualisation library for correlation analysis and creation of plots
                                                         
**[Numpy 1.26.4](https://numpy.org/)** Library for computing, providing a collection of mathematical functions to work on arrays

**[Pandas 1.5.3](https://pandas.pydata.org/)** Library to convert the source data into a DataFrame. Used for data management, data manipulation, and analysis of data structures

**[Pandas Profiing](https://pypi.org/project/pandas-profiling/)** is a tool that generates detailed reports of DataFrame structure with information about feature type, distribution, missing values, and correlations. Used in data_cleaning and correlation_study

**[Plotly 5.24.0](https://pypi.org/project/plotly/)** used to create graphs for exploring and presenting machine learning results in a deployed application.  

**[Ppscore 1.3.0](https://pypi.org/project/ppscore/)** used to calculate relationships between feature pairs in the dataset and Predictive Power Score Analysis

**[Python](https://www.python.org/)** Python is an interpreted, high-level and general purpose programming language

**[Seaborn 0.11.0](https://seaborn.pydata.org/)** Data visualization library. Used to prepare statistical graphs such as heatmaps. Library expands the functionalities of matplot-lib

**[Scikit-learn 1.5.1](https://scikit-learn.org/stable/index.html)** used to train and evaluate the ML model. Training with Scikit-learn includes corss validation and hyperparameter optimisation to identify the best model and to determine the best parameters for model performance

**[Streamlit 1.40.1](https://streamlit.io/)** Open-source library to create and share we applications for machine learning and data science projects. Used to create the dashboard to display separate pages of the project and interactive page with widgets for prediction of a house sale price

**[XGBoost 1.2.1](https://pypi.org/project/xgboost/)** used to build gradient boosting models to ensure accurate predictions in a deployed machine learning application.  

## Credits

### Code

The following functions from CI training videos on ML and walkthrough project 2 were used in the project:

* Evaluate MissingData funciton from under the heading "Data Cleaning" and "Assessing Missing Data Levels"
* DataCleaningEffect function from under the heading "Data Cleaning"
* Functions heatmap_corr(), heatmap_pps(), CalculateCorrAndPPS(), and DisplayCorrAndPPS() taken from CI ProdictePowerScore Unit1: Introduction, Video No. 6
* Functions to create plots (inside 03_correlation_study.ipynb) taken from walktrhough project 2 (churned customer study)
* Functions in correlation_analysis_page.py such as heatmap_corr(), heatmap_pps(), CalculateCorrAndPPS(), DisplayCorrAndPPS() from walkthrough project
* Feature engineering custom function taken from CI feature engine unit 9: custom functions
* Custom class HyperparameterOptimizationSearch from CI walkthrough project
* The rain_test_split() function from CI Scikit-Learn Unit 3
* Function pipeline_linear_regression() from CI Scikit-Learn Unit 3
* Evaluation of regressor pipeline (regression_performance(), regression_evaluation(), regression_evaluation_pluts() from CI Scikit-Learn Unit 3)
* Function PipelineOptimization() with multiple optimizations from CI walkthrough project and CI Scikit-Learn Unit 6

The following resources were used to better understand the different steps of the ML pipeline or statistical concepts

**[ML-Mastery](https://machinelearningmastery.com/feature-relationships-101/)** This article provided me a good overview over the relationships
of features in the Ames Housing dataset.

The book "Statistics for business and economics" by Anderson/Sweeney/Williams, 7th edition, 1999. Even though this seems a "dated" source the
statistical concepts for Multiple Regression and Regression Analysis are explained well in this book, thus improving my overall understanding how to address
the underlying project goal

### Media

The image used at the start of the README was created with Mult Device Website Mockup generator Techsini

### **Content**

- The iniital draft of this documentation was taken from a **[code repository](https://github.com/Code-Institute-Solutions/milestone-project-heritage-housing-issues)** provided by **[Code Institute](https://codeinstitute.net)**

## Acknowledgements

* I want to thank my mentor, Mo Shami, for the support on the project.