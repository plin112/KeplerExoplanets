# KeplerExoplanets

## Presentation

### Selected topic
Exoplanet — searching for a new World beyond our solar system

### Reason why the topic has been selected
Is Earth the only habitable planet in the universe? Scientists and researchers are searching for planets that can provide similar living conditions for human, and those planets are called “exoplanet”. We want to investigate the exoplanet data provided by NASA Exoplanet Archive and find a habitable planet. 

### Description of the source of data
* https://exoplanetarchive.ipac.caltech.edu/index.html
* https://www.kaggle.com/nasa/kepler-exoplanet-search-results

### Questions we hope to answer with the data
* How many confirmed planets?
* What type of planets consider as confirmed planets? 
* Which confirmed planet is closest to Earth?
* What are the characteristics of confirmed planets? 
* Based on the characteristics, which confirmed planet is the most habitable? 
* What are the most recent discovered confirmed planets? 
* How often are exoplanets confirmed in the existing liteatures disconfirmed by measurement from Kepler?

Google slides drafting:
https://docs.google.com/presentation/d/1aQ9Man76uhiFXY43nu5pnqOB6zrk1MvBqSxHWUtZ_Y0/edit?usp=sharing

## GitHub
### Communication protocols
After each pull request (PR), the person in charge of the github repository will review the code and ask for team assistance if necessary.
![review_process.png)](images/github/review_process.png)

After the PR has been accepted, the person who made the PR will merge her/his code to the main branch and alert the team that their own personal branch or sub-branch needs to be updated with the latest version of the main branch.
![github_merge.png)](images/github/github_merge.png)


## Machine Learning Model
Our target result is binary: Is it a planet or not. The dataset is labeled (koi_pdisposition).

#### Based on the Dataset we will be evaluating the below (4) models.
|Model name|Benefits|Limits|
|---|--|--|
|Supervised ML logistic Regression|- Easy to understand predictions| - Could struggle with high dimensional datasets and correlated features|
|Gradient Boosted Tree|- High-performing<br> - Easy to understand predictions|- Sensitive to outliers|
|Random Forest|- High-performing<br>- Robust against overfitting<br>- Fast to train|- Not easy to understand predictions|
|Neural Net (Sigmoid activation)|- Handle extremely complex tasks|- Slow to train<br>- Almost impossible to understand predictions|


#### EDA & Preprocessing
Null Values
- A large number of Null values (40k+)are present in the raw data. After preprocessing (including dropping unneeded columns) 3,572 remain
- We are evaluating several methods for handling these: Dropping, Imputing (Mean, Median, Mode)

Feature Evaluation & Selection
- We are primarily using a Sequential Feature Selector currently from the mlextend library. This performs an analysis on a range of possible features subset and scores them. Additionally we have a Correlation Matrix, Coefficient analysis and Feature Importance Graph to guide feature selection

Creating test & train datasets
- Initially we set the targey(y) to koi_pdisposition and the features to the remaining columns based on the feature evaluation process
- The training & testing set are split in default manner which works out to 75% train & 25% test

Scaling
- The processed dataframe is scaled using ScikitLearns's standard scaler before the models are ran

## Database
We are using the Postgres DB, currently an instance running in AWS on a free tier.

The DB engine instance is called "kepler", with two tables
- "raw_kepler" & **XXXX**
- raw_kepler is populated wth the CSV data file sourced from kaggle
- **XXXX** is a populated with ...................!!!!

Project DB files of note:
- The DB & table definition SQL files are in the project Database folder.
- The source CSV file is in the project Resources folder.
- The source CSV file was copied from this kaggle source - https://www.kaggle.com/nasa/kepler-exoplanet-search-results?select=cumulative.csv

We used the PG Admin console Import/Export tool to import the CSV file into the raw_kepler DB table.
An initial load resulted in the following outcome:
- "Successfully run. Total query runtime: 215 msec. 9564 rows affected."

### DB Schema
- The column "kepoi_name" is the "raw_kepler" table's unique primary key.
- The column "kepid" is the "habitable_data" table's primary ky.
- **XXXXhabitable_data** is joined to raw_kepler using the kepid as a foreign key. 
- This is a one to many relationship, as there may be more than one Kepler Object of Interest associated with any kepid star.

ERD - ![see here](https://github.com/tom-jj-G/KeplerExoplanets/blob/main/Database/ERD.jpg)

- Data dictionary "Data Columns in Kepler Objects of Interest Table" is located here "https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html#tce_info"


## Dashboard
Google slides drafting: https://docs.google.com/presentation/d/1aQ9Man76uhiFXY43nu5pnqOB6zrk1MvBqSxHWUtZ_Y0/edit?usp=sharing
![](images/github/dashboardDraft.png)

We are currently planning on using Tableau for the presentation & dashboard. The interactive elements will be the graphs shown.
