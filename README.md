### GDP PREDICTION PROJECT

#### PROJECT OBJECTIVE<br>
To create a GDP prediction model by the most significant 5 variables.

#### FINAL GDP PREDICTION MODEL AND RESULTS <br>

* ###### SELECTED THE MOST SIGNIFICANT VARIABLES:
1. 'General government revenue / Percent of GDP / '; 
2. 'General government total expenditure / National currency / Billions'; 
3. 'Gross national savings / Percent of GDP / '; 
4. 'Total investment / Percent of GDP / ';
5. 'Unemployment rate / Percent of total labor force / '; 

* ###### SCOPE OF SELECTED DATA:
EU members countries

* ###### OUTLIERS:
Dropped data of Luxemburg

* ###### MODEL RESULTS:
**BY ALL VARIABLES**
>***LinearRegression***:<br>
MSE : 18171.6536<br>
MAPE : 0.59187<br>
> 
>***XGBoost***:<br>
MSE : 4672.7466<br>
MAPE : 0.11727<br>
> 
>***XGBoost-GridSearchCV***:<br>
MSE : 4321.8728<br>
MAPE : 0.11890<br>

**BY SELECTED VARIABLES**
>***LinearRegression***:<br>
MSE : 18467.6556<br>
MAPE : 0.61706<br>
> 
>***XGBoost***:<br>
MSE : 15833.3957<br>
MAPE : 0.33534<br>
> 
>***XGBoost-GridSearchCV***:<br>
MSE : 16086.2188<br>
MAPE : 0.33218<br>

**BY SELECTED VARIABLES WITHOUT OUTLIERS**
>***LinearRegression***:<br>
MSE : 10813.3047<br>
MAPE : 0.69535<br>
>
>***XGBoost***:<br>
MSE : 5189.1234<br>
MAPE : 0.29164<br>
>
>***XGBoost-GridSearchCV***:<br> 
MSE : 5189.1234<br>
MAPE : 0.29164<br>

* ###### SELECTED MODEL FOR GDP PREDICTION:
Model with the best performance : ***XGBoost with GridSearch***<br>
By : ***selected features without outliers***.

#### <span style='background :powderblue' > RUN PROJECT</span>
1. Download full content of documents;
2. Install 'requirements.txt';
3. Run 'model.py' from folder 'flask_app';
4. Run 'app.py' from folder 'flask_app';
5. Congratulations! API server is running. Please predict GDP now. 
6. Run 'GDP_model.ipynb' for overview full project implementation.

#### <span style='background :powderblue' > CONTENT OF 'GDP_MODEL.ipynb'</span>

#### USED FUNCTIONS
* ###### FOR PLOTTING:
> ***def label_point*** : setting data labels in plots;<br>
> ***def plot_with_trend*** : plotting of dependent and independent variables with trend line;<br>
> ***def clusters_plot*** : plotting of predicted clusters + counting and plotting top_n of variables; <br>
> ***def pred_err_plot*** : plotting regression results (real value vs predicted value/prediction error);<br>
* ###### FOR CLUSTERING:
> ***def clusters_no_scale*** : clustering without data scaling (not recommended);<br>
> ***def clusters_scale*** :  clustering with data scaling (recommended);<br>
> ***def Elbow*** : Elbow method to find optimal number of clusters; <br>
* ###### FOR REGRESSION MODEL:
> ***def OLS_model*** : Ordinary Least Squares (OLS) regression;<br>
> ***def PooledOLS_model*** : PooledOLS regression - basic regression on panel data;<br>
> ***def model_results*** : regression model measures (MSE & MAPE);<br>
> ***def LinReg_model*** : Linear regression;<br>
> ***def XGB_model*** : Extreme Gradient Boosting (XGBoost);<br>
> ***def XGB_Grid_model*** : Extreme Gradient Boosting (XGBoost) with GridSearch;<br>
* ###### FOR GDP PREDICTION:
> ***def GDP_prediction*** : GDP prediction by input values (final XGB_Grid_model);<br>

#### 1. DATA INPUT : LOADING AND CLEANING
> ***df*** : International Monetary Fund, IMF (main Data);<br>
> ***df_cont_list*** : Countries By Continent (additional Data);<br>
> ***df_all*** : Merged Data (main data/Country + additional data/Continent);<br>
> ***df_GDP*** : GDP Data (Gross Domestic Product Per Capita, current prices);<br>
> ***oecd_country_list*** : OECD Members List;<br>
> ***eu_country_list*** : EU Members List;<br>

#### 2. DATA ANALYSIS 
###### 2.1. BASIC DATA ANALYSIS AND CHECK
> • 'ESTIMATES START AFTER': Analysis Of Actual And Predicted Data Quantity<br>
> • 'ESTIMATES START AFTER': Analysis Of Actual And Predicted Data Quantity By Continent<br>
> • Number Of Continent Check In Diffrent Dataframe<br>
###### 2.2. Exercise #1
> Raskite top 10 šalių, kurių "Gross domestic product per capita" paaugo daugiausiai.<br>
>> ***Result (output)*** : DataFrame 'df_GDP1' (calculated and submitted GDP growth by U.S. dollars and % difference of selected years period). 
###### 2.3. Exercise #2
> *i)* Nubraižykite grafiką, kaip augo OECD šalių populiacija per paskutinius 10 metų.<br>
> *ii)* Išsaugokite visus grafikus pagal šalis kaip png failus.
>> ***Result (output)*** : plotted population of OECD members and figures saved by one in new created folder. 
###### 2.4. Exercise #3
> *i)* Padalinkite šalis į 5 klasterius pagal GDP ir "Volume of exports of goods".<br>
> *ii)* Nubraižykite klasterius (GDP x-ašis ir Volume y-ašis).<br>
> *iii)* Pažymėkite top 5 šalis pagal GDP kiekviename klasteryje ir pridėkite tekstinį žymeklį.<br>
>> ***Result (output)*** : implemented clustering by given exercise and more :)
###### 2.5. Exercise #4
> Raskite visas metrikas, kurios nėra tuščios 2015 metų duomenyse.<br>
>> ***Result (output)*** : list 'df4_features' (list of features which are not null in column "2015").

#### 3. GDP PREDICTION MODEL COMPOSITION
##### 3.1. DATA PREPARATION
> • Selecting And Cleaning<br>
> • Pivoting (preparing final DataFrame for Regression Models)<br>
> • Analysis of ISNA() Quantity<br>
>> ***To many Nan values of all countries, so were selected only EU members.***<br>
> 
> • EU MEMBERS DATA : Selecting<br>
> • EU MEMBERS DATA : Cleaning / Replacing<br>
##### 3.2. GDP PREDICTION MODEL
##### 3.2.1. FEATURES SELECTION
> • Visual Analysis Of GDP Dependency From All Subjects<br>
> • Identification Significant And Insignificant Factors - Ordinary Least Squares (OLS)<br>
> • Selection of Significant Factors - Ordinary Least Squares (OLS)<br>
> • Visual Analysis Of GDP Dependency From Selected Subjects As The Most Significant<br>
> • Splitting Data : TRAIN & TEST<br>
> • Cross_Validation : Check For Other Option For The Most Significant Variables<br>
> • PooledOLS (Panel Data Model) : Results Check <br>
##### 3.2.2. GDP PREDICTION MODEL RESULTS
* ###### A. RESULTS BY ALL FEATURES<br>
> • LinearRegression<br>
> • XGBoost<br>
> • XGBoost-GridSearch<br>
> • • • COMPARISON OF RESULTS<br>
* ###### B. RESULTS BY SELECTED FEATURES<br>
> • LinearRegression<br>
> • XGBoost<br>
> • XGBoost-GridSearch<br>
> • • • COMPARISON OF RESULTS<br>
##### 3.2.3. OUTLIERS ANALYSIS
> •  Analysis Of GDP Outliers;<br>
> •  Histograms of GDP Before And After Removing Outliers;<br>
> •  Splitting Data Without Selected Outliers To Train & Test;<br>
* ###### C. RESULTS BY SELECTED FEATURES WITHOUT OUTLIERS
> • LinearRegression<br>
> • XGBoost<br>
> • XGBoost-GridSearch<br>
> • • • COMPARISON OF RESULTS<br>

#### 4. GDP PREDICTION MODEL EXECUTION
> •  Saving Data Without Outliers For Data Reuse In Flask App;<br>
> •  Selected Variables Data Without Outliers Of EU Members (FYI);<br>
> •  GDP Prediction By Input Values;<br>