Classifying World Economies

Version 1.0
Updated: June 09, 2024

------------------------------------------------------------------------------

README CONTENTS
0.1 Contact Information

1.0 Release Contents
1.1 Introduction
1.2 Acknowledgements
1.3 Rights Information
1.4 Using this Database
1.5 Revision History

2.0 Data Tables
2.1 Original IMF Format
2.2 Processed Data Set Features
2.3 Target
2.4 Supervised Algorithms
2.5 Clustering

3.0 Results
3.1 Supervised Results
3.2 Clustering
3.3 Conclusion

4.0 Appendix
4.1 Advanced Countries List
4.2  Developing Countries List

------------------------------------------------------------------------------
0.1 Contact Information

Name:                Email:
David Blankenship:   dwb65@drexel.edu
Jai Vaidya:          jv625@drexel.edu

------------------------------------------------------------------------------
1.0  Release Contents

The contents of this dataset is listed below
      readme.txt     
      WEOOct2023allfix.xlsx
      G11_Project_Notebook.ipnyb      
      Classifying World Economies.pptx
      forest_model.sav
      log_model.sav
      tree_model.sav


------------------------------------------------------------------------------
1.1 Introduction
Our goal for this project was to see if we could verify the classification of
different countries as Advanced or Developing using real data and see if
there are other potential categories being missed. We approached this using
two methods:

Supervised, predictive classification of whether a country is a
developing/emerging or advanced economy.

Unsupervised clustering to determine if there is another classification schema
that could reasonably describe the data or see if the advanced and
developing/emerging paradigm appears spontaneously from the data.

------------------------------------------------------------------------------
1.2 Acknowledgements

This project was created thanks to the collaborative efforts of David
Blankenship and Jai Vaidya. This was originally created for their DSCI 631
class project at Drexel University in the Spring 2024 class. 

------------------------------------------------------------------------------
1.3 Rights Information

International Monetary Fund
The original data source was the World Economic Outlook Oct 2023 dataset made
by the IMF. It is available at their website listed here:

https://www.imf.org/en/publications/weo 

------------------------------------------------------------------------------
1.4 Using this Database

This version of the database is available in a comma-separated value format. 
This data was put together in a Python 3 environment. Specifically, the
Anaconda and Jupyter Notebook environment using the following packages:

Pandas
Numpy
Sci-kit learn
matplotlib
seaborn
joblib

It is recommended to import the data into your environment from the
provided data files and begin analysis from there. For Python 3, we recommend
importing the .xlsx file in as a pandas Dataframes using Panda's read_excel()
function as outlined in the Jupyter Notebook and along with the functions
defined in our EDA section to manipulate the data into the appropriate shape. 

------------------------------------------------------------------------------
1.5 Revision History

     Version      Date            Comments
       1.0        June 2024       Initial release for DSCI 631 class project   

------------------------------------------------------------------------------
2.0 Data Tables

The dataset that we used is the International Monetary Fund (IMF) World
Economic Outlook (WEO) dataset. 

It is a biannual dataset released by the IMF that is used to project economic
forecasts in the near and medium term. In addition to the forecast, it's also
a great collection of past economic data collected by the IMF. 

It has data past data from 1980 up to 2021 and continues with predictions
from there. It contains 44 features for 196 countries.


------------------------------------------------------------------------------
2.1 Original IMF Format

Initially all the data is shaped such that the rows are the features for every
country stacked on top of one another while the columns are the years and
various columns for the features like units, descriptions and so on.

------------------------------------------------------------------------------
2.2 Processed Data Set Features

We preprocess the dataset to remove employment in persons, as it is only
collected by advanced economies and two columns that would be duplicated after
coversion of national currencies to US dollars.

0   Gross domestic product, constant prices in US dollars
1   Gross domestic product, constant prices in Percent change
2   Gross domestic product, current prices in U.S. dollars
3   Gross domestic product, current prices in Purchasing power parity;
    international dollars
4   Gross domestic product, deflator in Index
5   Gross domestic product per capita, constant prices in US dollars
6   Gross domestic product per capita, constant prices in Purchasing power
    parity; 2017 international dollar
7   Gross domestic product per capita, current prices in U.S. dollars
8   Gross domestic product per capita, current prices in Purchasing power
    parity; international dollars
9   Gross domestic product based on purchasing-power-parity (PPP) share of
    world total in Percent
10  Implied PPP conversion rate in National currency per current international
    dollar
11  Total investment in Percent of GDP
12  Gross national savings in Percent of GDP
13  Inflation, average consumer prices in Index
14  Inflation, average consumer prices in Percent change
15  Inflation, end of period consumer prices in Index
16  Inflation, end of period consumer prices in Percent change
17  Volume of imports of goods and services in Percent change
18  Volume of Imports of goods in Percent change
19  Volume of exports of goods and services in Percent change
20  Volume of exports of goods in Percent change
21  Unemployment rate in Percent of total labor force
22  Population in Persons
23  General government revenue in US dollars
24  General government revenue in Percent of GDP
25  General government total expenditure in US dollars
26  General government total expenditure in Percent of GDP
27  General government net lending/borrowing in US dollars
28  General government net lending/borrowing in Percent of GDP
29  General government structural balance in US dollars
30  General government structural balance in Percent of potential GDP
31  General government primary net lending/borrowing in US dollars
32  General government primary net lending/borrowing in Percent of GDP
33  General government net debt in US dollars
34  General government net debt in Percent of GDP
35  General government gross debt in US dollars
36  General government gross debt in Percent of GDP
37  Gross domestic product corresponding to fiscal year, current prices in US
    dollars
38  Current account balance in U.S. dollars
39  Current account balance in Percent of GDP

------------------------------------------------------------------------------
2.3 Target

We have a target variable set to 0 or 1 depending on whether the country is
classified by the IMF as Developing or Advanced economies respectively.

See appendices for lists of the different countries in each category.

------------------------------------------------------------------------------
2.4 Supervised Algorithms

We implement a 5-fold cross-validation and a test split of 20%.

All models used K Nearest Neighbors = 3 for imputation of missing data points
and recursive feature elimination for feature selection.

We used the following algorithms for the supervised learning with the
selected hyperparameters:

Logistic Regression
  Recursive Feature Elimination
    Number of features to select: 1.0
    Steps: 0.1
  Model
    Penalty: L1
    C: 100

Decision Tree
  Recursive Feature Elimination
    Number of features to select: 0.1
    Steps: 0.5
  Model
    Max Depth: 10
    Minimum Samples Split: 2
    Minimum Samples Leaf: 1

Random Forest
  Recursive Feature Elimination
    Number of features to select: 0.75
    Steps: 1
  Model
    Max Depth: 10
    Minimum Samples Split: 2
    Minimum Samples Leaf: 1


------------------------------------------------------------------------------
2.5 Clustering

Before model building, K Nearest Neighbors = 3 is used for imputation of missing data points.
PCA was then performed and 1st 2 components were fed into the models.

We used the following algorithms:

K Means Clustering
  Elbow Plot and Silhouette Score Plot to identify optimal K
    Score for k = 2: -11803.636634895442
    Score for k = 3: -3640.8314135269616

DBSCAN
  min_samples = 5
  eps = 0.1, 0.2...0.8

Agglomerative Clustering
  n_clusters = 2
  Linkages used = "ward", "average", "complete", "single"

Gausian Mixture
  n_components=2
  covariance types = "full", "spherical", "diag", "tied"
  AIC/BIC plot to identify optimal K
  Best k: 5
  Best Covariance Type: full

------------------------------------------------------------------------------
3.0 Results

This section provides a summary of the results for each analysis, the process
to achieve these results, and a description of the challenges for each.

------------------------------------------------------------------------------
3.1 Supervised Results

Test Scores for Logistic Regression Model:
F1 Score (Test): 0.8311688311688312
Precision (Test): 0.8888888888888888
Recall (Test): 0.7804878048780488

Test Scores for Decision Tree Model:
F1 Score (Test): 0.9487179487179488
Precision (Test): 1.0
Recall (Test): 0.9024390243902439

Test Scores for Random Forest Model:
F1 Score (Test): 0.975609756097561
Precision (Test): 0.975609756097561
Recall (Test): 0.975609756097561

------------------------------------------------------------------------------
3.2 Clustering

K means (k=2)
normalized_mutual_info_score: 0.3955383189940556
adjusted_rand_score: 0.5777688363613122

DBSCAN
normalized_mutual_info_score: 0.05236904420828541
adjusted_rand_score: 0.09107931503444604

Agglomerative Clustering
normalized_mutual_info_score: 0.00743805187377737
adjusted_rand_score: 0.020076125670635537

Gaussian Mixtures
normalized_mutual_info_score: 0.17598207568900548
adjusted_rand_score: 0.3344522403257472


------------------------------------------------------------------------------
3.3 Conclusion
Overall, we are very satisfied with the results of our project. We set out to
verify if the advanced/developing dichotomy was verifiable by the data and we 
were to find exactly this to a very high degree of fidelity with the
supervised models. For the clustering models we saw that the clustering performance 
varies significantly across different algorithms.  K-Means achieved the highest scores, 
indicating moderate alignment with the ground truth labels. Gaussian Mixtures performed 
moderately well. DBSCAN and Agglomerative Clustering showed poor performance, 
with particularly low scores for Agglomerative Clustering suggesting its clusters are almost 
random compared to the true labels.  Overall, K-Means proved to be the most effective 
clustering method for this dataset.

------------------------------------------------------------------------------
4.0  Appendix

The appendix contains extra information that may be valuable for understanding
the dataset.

------------------------------------------------------------------------------
4.1 Advanced Countries List

Andorra
Australia
Austria
Belgium
Canada
Croatia
Cyprus
Czech Republic
Denmark
Estonia
Finland
France
Germany
Greece
Hong Kong SAR
Iceland
Ireland
Israel
Italy
Japan
Korea
Latvia
Lithuania
Luxembourg
Macao SAR
Malta
Netherlands
New Zealand
Norway
Portugal
Puerto Rico
San Marino
Singapore
Slovak Republic
Slovenia
Spain
Sweden
Switzerland
Taiwan Province of China
United Kingdom
United States

------------------------------------------------------------------------------
4.2  Developing Countries List

Afghanistan
Albania
Algeria
Angola
Antigua and Barbuda
Argentina
Armenia
Aruba
Azerbaijan
The Bahamas
Bahrain
Bangladesh
Barbados
Belarus
Belize
Benin
Bhutan
Bolivia
Bosnia and Herzegovina
Botswana
Brazil
Brunei Darussalam
Bulgaria
Burkina Faso
Burundi
Cabo Verde
Cambodia
Cameroon
Central African Republic
Chad
Chile
China 
Colombia
Comoros
Democratic Republic of the Congo 
Republic of Congo
Costa Rica
Côte d'Ivoire
Djibouti
Dominica
Dominican Republic
Ecuador
Egypt
El Salvador
Equatorial Guinea
Eritrea
Eswatini
Ethiopia
Fiji
Gabon
The Gambia
Georgia
Ghana
Grenada
Guatemala
Guinea
Guinea-Bissau
Guyana
Haiti
Honduras
Hungary
India
Indonesia
Islamic Republic of Iran
Iraq
Jamaica
Jordan
Kazakhstan
Kenya
Kiribati
Kosovo
Kuwait
Kyrgyz Republic
Lao P.D.R.
Lebanon
Lesotho
Liberia
Libya
Madagascar
Malawi
Malaysia
Maldives
Mali
Marshall Islands
Mauritania
Mauritius
Mexico
Micronesia
Moldova
Mongolia
Montenegro
Morocco
Mozambique
Myanmar
Namibia
Nauru
Nepal
Nicaragua
Niger
Nigeria
North Macedonia
Oman
Pakistan
Palau
Panama
Papua New Guinea
Paraguay
Peru
Philippines
Poland
Qatar
Romania
Russia
Rwanda
Samoa
São Tomé and Príncipe
Saudi Arabia
Senegal
Serbia
Seychelles
Sierra Leone
Solomon Islands
Somalia
South Africa
South Sudan
Sri Lanka
St. Kitts and Nevis
St. Lucia
St. Vincent and the Grenadines
Sudan
Suriname
Syria - Of note Syria is dropped in our dataset due to no data being collected
        since 2011 due to the ongoing Syrian Civil War
Tajikistan
Tanzania
Thailand
Timor-Leste
Togo
Tonga
Trinidad and Tobago
Tunisia
Türkiye
Turkmenistan
Tuvalu
Uganda
Ukraine
United Arab Emirates
Uruguay
Uzbekistan
Vanuatu
Venezuela
Vietnam
West Bank and Gaza
Yemen
Zambia
Zimbabwe

<end of file>
