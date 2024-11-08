## Heritage House Sales Price Prediction

This project aims to understand and predict house prices by analyzing various factors that contribute to the sale price. We explore the relationships between house attributes and sale prices using statistical techniques like correlation analysis. Through this investigation, we aim to validate specific hypotheses and uncover key drivers that influence house prices in Ames, Iowa.

**<span style="color:red;">Reminder: insert the Techsini picture here once the dashboard is deployed**</span>

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
  - [6. Dashboard Design](#6-dashboard-design)
  - [7. Unfixed Bugs](#7-unfixed-bugs)
  - [8. Deployment](#8-deployment)
    - [Heroku](#heroku)
  - [9. Packages and technologies used](#9-packages-and-technologies-used)
    - [Technologies used:](#technologies-used)
  - [Main Data Analysis and Machine Learning Libraries](#main-data-analysis-and-machine-learning-libraries)
  - [Credits](#credits)
    - [Code](#code)
    - [Content](#content)
    - [Media](#media)
  - [Acknowledgements (optional)](#acknowledgements-optional)

## 1. Dataset Content

* The dataset is sourced from [Kaggle](https://www.kaggle.com/codeinstitute/housing-prices-data). Fictitious user stories were created where predictive analytics can be applied in a real project in the workplace.
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

Larger properties tend to have higher absolute sale prices. We will investigate correlations between attributes related to house size (e.g., square footage, number of bedrooms) and sale price to validate this hypothesis.

o	<span style="color:red; font-weight: bold;">Validation Result: Hypothesis confirmed/not confirmed. Are features such as '1stFlrSF', 'GarageArea', 'GrLivArea' 'TotalBsmtSF' strongly correlated?</span>

2.	Overall Quality Hypothesis:
We suspect that the overall quality of a house will significantly impact the sale price. The higher the quality rating, the higher the expected sale/market price.

o	<span style="color:red; font-weight: bold;">Validation Result: Hypothesis confirmed/not confirmed. Are features such as 'KitchenQual_TA' and 'OverallQual' or other 'Qual' features strongly correlated?</span>

3.	Overall Condition Hypothesis:
We suspect that the overall condition of a house will influence the sale price. Houses in better condition should command a higher price.

o	<span style="color:red; font-weight: bold;">Validation Result: Hypothesis confirmed/not confirmed. Keep in mind that overall condition has overlap with remodel work/date/timing of remodeling work</span>

## 4. Rationale to map the business requirements to the Data Visualisations and ML tasks

* List your business requirements and a rationale to map them to the Data Visualisations and ML tasks.

## 5. ML Business Case

* Frame the business case using the method we covered in the course.
* Use the proper ML terminology such as labels, targets, features, variables, train
* ML pipeline to include the regressor model and live data data to estimate sales prices through input widgets

## 6. Dashboard Design

* List all dashboard pages and their content, either blocks of information or widgets, like buttons, checkboxes, images, or any other items that your dashboard library supports.
* Eventually, during the project development, you may revisit your dashboard plan to update a given feature 

## 7. Unfixed Bugs

* You will need to mention unfixed bugs and why they were not fixed. This section should include shortcomings of the frameworks or technologies used. Although time can be a big variable to consider, paucity of time and difficulty understanding implementation is not valid reason to leave bugs unfixed.

## 8. Deployment

### Heroku

* The App live link is: <https://YOUR_APP_NAME.herokuapp.com/>
* Set the runtime.txt Python version to a [Heroku-20](https://devcenter.heroku.com/articles/python-support#supported-runtimes) stack currently supported version.
  
* The project was deployed to Heroku using the following steps.

1. Log in to Heroku and create an App
2. At the Deploy tab, select GitHub as the deployment method.
3. Select your repository name and click Search. Once it is found, click Connect.
4. Select the branch you want to deploy, then click Deploy Branch.
5. The deployment process should happen smoothly if all deployment files are fully functional. Click the button Open App on the top of the page to access your App.
6. If the slug size is too large then add large files not required for the app to the .slugignore file.

## 9. Packages and technologies used
                                                           
### Technologies used:

**[Git](https://git-scm.com/)** The version control system Git was used to document the development of the application and to push code to the GitHub repository. The specific reasons for the commit are reflected in the respective commit message

**[GitHub](https://github.com/)** The code files, README files, and assets are stored on GitHub. The code on GitHub was pushed from Git
                                                            
**[Heroku](https://www.heroku.com/)** Heroku is a platform as a service (PaaS) to build, run, and operate applications cloud-based. It was used to deploy the website

**[Techsini](https://techsini.com/multi-mockup/)** Multi Device Website Mockup generator
           
**[Visual Studio Code](https://code.visualstudio.com/)** Visual Studio Code (VS-Code) was used as integrated development environment (IDE) for the entire project. The GitHub repository was cloned to VS-Code for this purpose	


## Main Data Analysis and Machine Learning Libraries											

The version number of the libraries used can be found in the [requirements file](https://github.com/Werner-Staeblein/Project-5/blob/main/requirements.txt) of this project.

**[Jupiter Notebooks](https://jupyter.org/)** Open-source web app to create and share documents
                                                            
**[Kaggle 1.6.12](https://pypi.org/project/kaggle/)** Tool for download of dataset from Kaggle
                                                            
**[Matplotlib 3.4.3](https://matplotlib.org/)** Data visualisation library for correlation analysis															
                                                         
**[Numpy 1.19.5](https://numpy.org/)** Library for computing, providing a collection of mathematical functions to work on arrays

**[Pandas 1.3.5](https://pandas.pydata.org/)** Library for data manipulation and analysis with data structures to handle structured data.

**[Python](https://www.python.org/)** Python is an interpreted, high-level and general purpose programming language

**[Streamlit 1.34.0](https://streamlit.io/)** Open-source library to create and share we applications for machine learning and data science projects

## Credits

* In this section, you need to reference where you got your content, media and extra help from. It is common practice to use code from other repositories and tutorials, however, it is important to be very specific about these sources to avoid plagiarism.
* You can break the credits section up into Content and Media, depending on what you have included in your project.

### Code

The following functions from walkthrough project 2 were used in the project

* Evaluate MissingData funciton from under the heading "Data Cleaning" and "Assessing Missing Data Levels"


The following resources were used to better understand the different steps of the ML pipeline or statistical concepts

**[ML-Mastery](https://machinelearningmastery.com/feature-relationships-101/)** This article provided me a good overview over the relationships
of features in the Ames Housing dataset.

The book "Statistics for business and economics" by Anderson/Sweeney/Williams, 7th edition, 1999. Even though this seems a "dated" source the
statistical concepts for Multiple Regression and Regression Analysis are explained well in this book, thus improving my overall understanding how to address
the underlying project goal


### Content

* The icons in the footer were taken from [Font Awesome](https://fontawesome.com/)

### Media

* The image used at the start of the README was created with the Multi Device Website Mockup generator Techsini 

## Acknowledgements (optional)

* In case you would like to thank the people that provided support through this project
* 

