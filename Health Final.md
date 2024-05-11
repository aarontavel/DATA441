# Determinants of Health and Perceptions of African Leaders

## Abstract:
This study investigates the correlations between food security, water security, healthcare access, and government perceptions in Lesotho, Namibia, and South Africa. Leveraging data from the AfroBarometer dataset, this research employs supervised machine learning techniques, including random forest regression and LOWESS, to analyze household-level data aggregated at the regional level. The 2030 Agenda for Sustainable Development serves as the backdrop, emphasizing the importance of addressing poverty, food insecurity, and health outcomes. Despite challenges including small sample sizes and missing data, permutation tests reveal statistically significant correlations between basic needs and perceptions of governance across the majority of regions studied. The implications extend to both data science and political science fields, highlighting the value of addressing small-n regression problems and emphasizing the pivotal role of basic services in fostering favorable perceptions of governance and political stability. Further, these findings suggest that individuals' views on governance are influenced by their access to essential services. Additionally, the study underscores the significance of basic needs in political stability. Supplemental analysis is warranted to explore regional variations and inform targeted policy interventions.

## Background:
The United Nations established the 2030 Agenda for Sustainable Development to outline a comprehensive framework for achieving "prosperity for people and the planet", comprising 17 Sustainable Development Goals (SDGs) (United Nations, 2015). These goals, along with 169 associated targets, advocate for eradicating poverty, addressing food and water insecurity, improving health outcomes, fostering good governance, and advancing various socio-economic developments.

In 2022, troubling statistics revealed significant global challenges in these areas. 149 million children faced stunted growth, with half of all deaths among children under five attributed to undernutrition (WHO, 2024). Simultaneously, nearly 2 billion individuals are forced to consume contaminated drinking water, resulting in an estimated 500,000 diarrhoeal deaths annually (WHO, 2023). Moreover, an alarming 4.5 billion people lack "essential health services" (WHO, 2023).

Africa, as a region, faces the lowest improvement in life expectancy and significant health disparities across its nations (Wamai and Shirley, 2023). These challenges are amplified by both weak health infrastructure stemming from minimal domestic investments and over-reliance on external aid. Consequently, ensuring universal access to essential healthcare services poses an ongoing challenge to achieving the Sustainable Development Goals by 2030.

This study focuses on three African countries: Lesotho, Namibia, and South Africa. Lesotho operates under a constitutional monarchy with a parliamentary system, characterized by a versatile political landscape due to frequent changes in government. Despite existing tensions between the monarchy, government, and military, the monarch does not exercise any executive power. As evaluated by the Freedom House (2024), Lesotho received a 30/40 score in political rights and a 36/60 in civil liberties, reflecting its challenges in these areas. Economically, Lesotho struggles as a low-income nation with severe food and water shortages, compounded by high unemployment rates; In 2022, only 28.22% of Basotho had consistent access to clean water (MacroTrends, 2022). The Healthcare Access and Quality (HAQ) Index, measuring a country's death rates based on avoidable mortality, indicates a 12% decline in Lesotho's HAQ Index from 1990 to 2015 (OurWorldInData, 2017).

Namibia, a democratic nation, has boasted political and economic stability since its independence and scored a 31/40 in political rights and 46/60 in civil liberties, outperforming Lesotho (Freedom House, 2024). Namibia has undergone peaceful transfers of power and does not face severe corruption. Nevertheless, Namibia grapples with persistent challenges such as an AIDS epidemic and racial tensions. Economically classified as a lower-middle-income economy, Namibia exhibits a notable disparity in per capita GDP between its Black and White populations (Britannica, 2024). Namibia has experienced a significant positive change in its HAQ Index from 1990 to 2019, increasing by 28%.

South Africa, a multi-party parliamentary democracy led by a President, surpasses its counterparts in political freedoms, scoring a 33/40 in political rights and 46/60 in civil liberties (Freedom House, 2024). However, the nation continues to struggle with its legacy of apartheid, racial tensions, and corruption. Despite being an upper-middle income country, South Africa still faces significant socio-economic challenges including high unemployment and enduring racial and economic inequalities (World Bank, 2024). From 1990 to 2015, South Africa's HAQ Index increased by 14%.

From a food security perspective, the three countries exhibit varying degrees of malnutrition. Lesotho faces the most severe malnutrition, with 46% of its population affected, followed by Namibia with 17.1% and South Africa with only 7.9% (World Population Review, 2024).

## Description of Dataset:
The dataset utilized in this study is sourced from the AfroBarometer, a valuable resource offering insights into various aspects of African societies. It includes data on public attitudes, experiences, and behaviors related to democracy, governance, economic conditions, and related issues. Covering a wide range of countries across Africa, the AfroBarometer serves as a crucial tool for researchers, policymakers, and organizations to understand public opinion trends and inform decision-making processes.

Since its inception in 1999, AfroBarometer has conducted nine rounds of surveys (AfroBarometer). These surveys provide data for individual countries across specific rounds, as well as merged datasets combining all countries for each round. For this study, merged data from rounds one through eight are leveraged, offering a comprehensive perspective on public sentiment and societal trends across multiple African nations.

A significant limitation of the dataset used in this study is its small sample size, comprising only eight time periods. This restriction imposed constraints on the algorithms that can effectively be used. Additionally, while the selected countries have nearly complete data, some regions are missing data for certain rounds.

## Data Preprocessing:

The dataset utilized in this study underwent extensive cleaning to prepare it for supervised machine learning. The following diagram illustrates the sequential cleaning conducted round-by-round.
**        ![](https://lh7-us.googleusercontent.com/KdMC1zu4lYbHsmq3QZa8gu5P68prFp9Z5aR9UYtGQlKSiq7Pk1olu6CMp1IS4Ecm4enXHryBm8vSwAzFlRASEMP8nsCoED-3Rz2AhUR96yHJcsS63mir8MMsLGcI_cCdx44x6z3EaG4EucyZqtGdIqQ)**
Notably, to facilitate the data merging, numerous variable labels were edited. Variations in the spelling of regions such as “Ville d’Abidjan,” “N’Zi Comoe,” and “N’zerekore” across rounds required additional research to identify the proper spelling. To ensure consistency, the Americanized version of the spelling was adopted. Subsequently, to create a dictionary mapping region codes (integers) to their corresponding names (strings), all apostrophes and special characters were manually removed. Moreover, the region codes and map codes underwent changes from round to round, requiring additional cleaning. A code snippet demonstrating this process is provided.

    combined_region_remapping = {'Kwazulu-Natal':'KwaZulu-Natal','KwaZulu Natal':'KwaZulu-Natal','Kwazulu-Natal':'KwaZulu-Natal', '!Karas':'Karas',
    
    'Buthe-Buthe':'Butha-Buthe', 'Botha-Bothe':'Butha-Buthe', 'hardap':'Hardap', 'Thaba Tseka':'Thaba-Tseka',
    
    'Qachas nek':'Qachas Nek', 'Kwa-Zulu Natal':'KwaZulu-Natal', 'ThabaTseka':'Thaba-Tseka', 'kavango':'Kavango West'}

  
Furthermore, slight variations in the questions asked from round to round required additional cleaning. Changes in the scale for respondent answers and the variable names for questions also occurred every round. Originally the target variable of interest was perceptions of governance; however, this question was only posed in select rounds. Consequently, adjustments were made to the study to change the target of interest to perceptions of prime ministers or presidents.


## Initial Statistics:
After cleaning data from eight rounds for Lesotho, Namibia, and South Africa, the merged dataset contained 36,747 records. Subsequent filtering for responses categorized as “unsure,” “refused,” or missing data resulted in 33,116 records, with 3,631  removed.

Lesotho contributed 8,300 records across 10 regions, with the highest number of responses from Maseru (2,019) and the lowest from Qacha's Nek (329). The predominant response for water security, access to healthcare, and perceptions of governance in Lesotho was "1" (never gone without food in the previous year). Interestingly, the most common response for food security was "3" (often gone without food in the past year).

Namibia provided 9,168 records across 13 regions, with the majority of responses from Khomas (1,430) and the fewest from Otjozondjupa (86). The most frequent response for water security, food security, and access to healthcare in Namibia was "1." However, for perceptions of governance, "2" (support prime minister) was the most common response.

South Africa contributed 15,648 records across 9 regions, with the highest number of responses from Gauteng (3,206) and the lowest from Mpumalanga (165). The modal responses for all four variables in South Africa mirrored those of Namibia.


|Variable | Codes | 
|--|--|
|food/water/health | 1: Never; 2: Occasionally/Sometimes/Rarely; 3: Frequently/Often; 4: Always; 97: Unsure; 98: Refused; 99: Missing |
| region | Value labels
|country | LES: Lesotho; NAM: Namibia; RSA: South Africa
|government| 1: Strongly Support Leader; 2: Support Leader; 3: Oppose Leader; 4: Strongly Oppose Leader;9 7: Unsure; 98: Refused; 99: Missing |

---
|  | food | water | health | government |
|--|--|--|--|--|
| Lesotho |1 = 2670;  2 = 1647; **3 = 3691**; 4 =  292   | **1 = 3648**;2 = 1178;3 = 2791;4 = 683| **1 = 3555**;2 = 1582;3 = 2874;4 = 289 |**1 = 2586**;2 = 2084;3 = 1145;4 = 2485  
| Namibia|**1 = 4302**;2 = 2137;3 = 2557;4 = 172|**1 = 5319**;2 = 1658;3 = 1892;4 = 299| **1 = 4655**;2 = 2281;3 = 2041;4 = 191|1 = 3461;**2 = 4310**; 3 = 975; 4 = 422 
|South Africa |**1 = 9431**; 2 = 3139; 3 = 2788; 4 = 290 |**1 = 10052**; 2 = 2212; 3 = 2590; 4 = 794 |**1 = 9661**; 2 = 2891; 3 = 2604; 4 = 492 | 1 = 2603;**2 = 6545**; 3 = 3990; 4 = 2510 
---

## Trends Round-to-Round:
Visualizations were created to depict trends in the modal responses for four variables across the three target countries (see Appendix A). Additionally, specific visualizations are provided for regions with the most responses in each country: Maseru, Lesotho; Khomas, Namibia; and Gauteng, South Africa. It is important to note that Khomas is missing data from Round 2, underscoring the limitations of my data.

The visualizations reveal that perceptions of governance exhibit greater variability compared to food security, water security, and access to health care. While this variability may be explained by political factors, my hypothesis posits that food and water security, along with healthcare access, are also statistically significant determinants.

## Methodology:

The research question under investigation is whether food security, water security, and access to healthcare serve as determinants in shaping perceptions of governance. The hypothesis proposes that there is a statistically significant correlation between the independent and dependent variables.

To test this hypothesis, a permutation test will be conducted on the strongest model identified through initial analysis.

Following data cleaning and initial analysis from the eight rounds of data and subsequent visualizations, four algorithms were evaluated as potential supervised machine learning models for predicting the perceptions of governance based on the independent variables. The selected algorithms for further analysis are Square Root Lasso, Elastic Net, LOWESS (Locally Weighted Scatterplot Smoothing), and Random Forests.
**![](https://lh7-us.googleusercontent.com/fQ-Q2r_Wmd2NIhe66kAmK_UKoHc9Mef0bzPTYVB_ZiFIX4E8t8GgqGUKGqz4ss4iBxD7PrdKiPlAkNsDd-kAs9GbW9QwIVWnJze_YqtwrtBlhOFiyL6QNdoFI9jHmURZeE9JhRQvHidL33vomta80s0)**

## Model Selection:

Scikit-learn, an open-source Python library for machine learning, was essential in this study. Functions from various modules within Scikit-learn, including preprocessing, metrics, ensemble, model_selection, decomposition, and base libraries were utilized throughout the project.

The method of analysis remained consistent across all four models. Initially, the dataset was subsetted by country and then organized into three dictionaries of smaller data frames, each corresponding to regions within their respective country. Subsequently, the root-mean-square-error (RMSE), which represents the standard deviation of the residuals, was computed for each region in the dictionary as well as the average RMSE for the entire country. The RMSE is a widely used metric for assessing the accuracy of a model's predictions, with lower values indicating better fit to the data.![](https://lh7-us.googleusercontent.com/TQyv1q_-TpNnOEHxmWMDrSEqiM97ZrxQxU_7O30BfYjwbv0Q1KmB-8lG2K-Ekv7cCKma6667WBUgW2pcDJmY-yybinVpsGFYmQC0La2UM6dfT2xDjfupw-pTIZRZlXpfuUl7uao-WEPDR92U3dH6So4)

Another significant downside of working with a small dataset is the inability to perform robust cross-validation on the models. Techniques such as k-fold validation, individual train-test splits, and leave-one-out cross-validations were explored but yielded poor results due to the limited size of the data.

Baseline analysis of the RMSE identified LOWESS and Random Forest as the only viable models for the dataset. A grid search analysis was then conducted using GridSearchCV() from sklearn.model_selection for both algorithms to determine the optimal hyperparameters. Subsequently, the models were re-evaluated based on their RMSE scores. Ultimately, the Random Forest Regressor was the model used in this study.

|  Machine Learning Algorithm|Optimal Hyperparameter  | RMSE
| -- | -- | --|
| Square Root Lasso|`num_epochs=500, learning_rate=0.01` |`1.868`| 
|Elastic Net |`alpha = 0.25, l1_ratio = 0.5, num_epochs=250, learning_rate=0.1` |`1.846`|
|LOWESS|`kernel = Quartic`|`1.318`|
|Random Forest|`n_estimators=100, max_depth=2`|`0.981`|

  
### Random Forest Regressor:
![](https://lh7-us.googleusercontent.com/tzDesb1hLryKG-elJyjo0EPLAKmFRX5ro2bSTl5Pz2wHFWUXF_jnnY_fEVCyEGDxK3HShFQxDy-z1JB8zeROTfpfnFi3KUD7yA-Wtt-9avrJ1Z2Ajz3IInG6XdaO5VFByBMWgcRJ56hcn-__qa1VOQ4)

Random forest regressor is an ensemble tree-based regression methodology that functions by constructing multiple forests, each containing trees that generate regressions. The final model is determined by aggregating the predictions from all trees and selecting the forest with the most votes (Alfaiad et al., 2023). In this study, the RandomForestRegressor() within the sklearn.ensemble  module was utilized to implement this algorithm.

Given the small sample size of the dataset, concerns regarding overfitting were essential to address. Overfitting occurs when a machine learning model "gives accurate predictions for training data but not for new data" (AWS). Small sample sizes often exacerbate this problem, as the algorithm may not have sufficient data to learn from effectively. Fortunately Leo Breiman, the creator of random forests, argued in his paper that "random forests do not overfit as more trees are added, but produce a limiting value of the generalization error. " (2001). Breiman’s claim asserts that random forests are robust to overfitting.

### Locally Weighted Scatterplot Smoothing (LOWESS):
**![](https://lh7-us.googleusercontent.com/LP7MQOJZI_Dl65nIefCEILabene_kwj-KPK7N5G5D0lz4mIAvrYYAkcJEw3pJVjeUeGXtw_QUUp0JpYJkBSY6075wGAeBmmGV8qtinz4QJ06p4Q4N3slZ50zjXjFTV9qvSwbJ26_g5Tt_CjSSoIrYXo)**
In this study, a custom implementation of LOWESS developed by Vasiliu was used. The primary motivation behind LOWESS is to perform nonparametric regression by employing a K-nearest neighbors approach at every data point. Here, smoothed curves are fitted to each data point by conducting the weighted regression on neighboring points. This approach captures local trends in the data while minimizing the impact of noise, thereby mitigating overfitting issues.


### Permutation Test:

After identifying the Random Forest as the optimal regression model for the hypothesis, a permutation test was conducted on the optimal hyperparameters across all regions. Permutation tests are preferred for their "minimal assumptions," making them well-suited for analysis with small datasets (Ottoboni et al., 2018). These tests aim to determine "the probability that the observed metric is a result of chance" (Camacho, 2016).

To execute the permutation test, each feature was individually selected and permuted a number of times, 100 in this study. Then, the root-mean-square-error was calculated for each permutation and both the mean and standard deviation of the aggregated RMSEs across all permutations were determined. A test statistic was then computed by the formula: (RMSE0-RMSEa)/std(RMSEa). Chebyshev's theorem was applied to establish bounds for the probability of the observed test statistic under the null hypothesis.

To calculate the p-values, the probability of the observed RMSE deviating from the aggregated RMSE mean by more than k standard deviations was determined by 1/k2. This approach ensures the derivation of significant p-values even with small sample sizes, as demonstrated in a similar small-n study that utilized Chebyshev’s inequality (Beasley, 2004).

  

## Results:

P-values were computed for the three independent variables across the three countries using the permutation test (Appendix B). A significance level of 10% was chosen to determine significant p-values. If a p-value is less than 10, it indicates that the permuted variable significantly influenced the RMSE, thereby demonstrating the statistical significance of the original column in predicting perceptions of governance. However, a limitation of this test is that any region missing data in a round will corrupt the test, resulting in “nan” values. Consequently, only 10 regions in Namibia were investigated due to complete data availability.

The table below summarizes the results of the permutation test, indicating the number of regions where each variable exhibits a statistically significant correlation with the dependent variable.

| Country | Food |Water | Health|
|--|--|-- |--|
| Lesotho | 10/10 | 8/10 |5/10 |
|Namibia | 7/10 | 8/10 | 8/10 | 
| South Africa | 7/9 | 8/9 | 9/9

Across all three countries, the vast majority of regions yielded statistically significant results, confirming a correlation between the independent variables and perception of governance. Therefore, I fail to reject the hypothesis that food security, water security, and access to health care are determinants of perceptions of governance.

## Discussion:

This study contributes to the literature on small-n regression problems. With a dataset only containing eight time periods, performing a time-series analysis was particularly challenging. However, by leveraging a random forest regressor and permutation tests, overfitting was addressed, leading to statistically significant results. As more rounds are released by the AfroBarometer dataset, future research can revisit this methodology with additional data to assess any significant changes in results.

From a political science perspective, this study holds significant implications. It suggests that individuals' perceptions of governance are influenced by their ability to meet basic needs. Governments that effectively address food insecurity, water scarcity, and healthcare access may enjoy greater public favor and political stability. Conversely, neglecting these essential needs could lead to discontent and potential instability, highlighting the importance of basic services in maintaining political stability.

Further analysis is warranted to explore why access to healthcare is statistically significant in only half of the regions analyzed while food security and water security are significant in all or most regions. This investigation could shed light on regional variations and inform targeted policy interventions.

## References:

“AIDS in Africa.” SOS Children’s Villages. [https://www.sos-usa.org/SpecialPages/Africa/AIDS-in-Africa](https://www.sos-usa.org/SpecialPages/Africa/AIDS-in-Africa) (May 9, 2024).

Beasley, T. Mark, Grier P. Page, Jaap P. L. Brand, Gary L. Gadbury, John D. Mountz, and David B. Allison. 2004. “Chebyshev’s Inequality for Nonparametric Testing with Small N and α in Microarray Research.” Journal of the Royal Statistical Society Series C: Applied Statistics 53(1): 95–108. doi:[10.1111/j.1467-9876.2004.00428.x](https://doi.org/10.1111/j.1467-9876.2004.00428.x).

Camacho, Francy Liliana, Rodrigo Torres-Sáez, and Raúl Ramos-Pollán. 2017. “Assessing the Behavior of Machine Learning Methods to Predict the Activity of Antimicrobial Peptides.” Revista Facultad de Ingeniería 26(44): 167–80. doi:[10.19053/01211129.v26.n44.2017.5834](https://doi.org/10.19053/01211129.v26.n44.2017.5834).

“Clean Water Access by Country.” [https://www.macrotrends.net/global-metrics/countries/ranking/clean-water-access-statistics](https://www.macrotrends.net/global-metrics/countries/ranking/clean-water-access-statistics) (May 10, 2024).

“Confidence Intervals for LOWESS Models in Python.” 2020. [https://james-brennan.github.io/posts/lowess_conf/](https://james-brennan.github.io/posts/lowess_conf/) (May 10, 2024).

“Drinking-Water.” [https://www.who.int/news-room/fact-sheets/detail/drinking-water](https://www.who.int/news-room/fact-sheets/detail/drinking-water) (May 9, 2024).

“Evaluating the Compressive Strength of Glass Powder-Based Cement Mortar Subjected to the Acidic Environment Using Testing and Modeling Approaches | PLOS ONE.” [https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284761](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284761) (May 10, 2024).

“Fact Sheets - Malnutrition.” [https://www.who.int/news-room/fact-sheets/detail/malnutrition](https://www.who.int/news-room/fact-sheets/detail/malnutrition) (May 9, 2024).

“Healthcare Access and Quality Index.” Our World in Data. [https://ourworldindata.org/grapher/healthcare-access-and-quality-index?tab=table](https://ourworldindata.org/grapher/healthcare-access-and-quality-index?tab=table) (May 10, 2024).

K, Gurucharan M. 2020. “Machine Learning Basics: Random Forest Regression.” Medium. [https://towardsdatascience.com/machine-learning-basics-random-forest-regression-be3e1e3bb91a](https://towardsdatascience.com/machine-learning-basics-random-forest-regression-be3e1e3bb91a) (May 10, 2024).

“Lesotho: Freedom in the World 2021 Country Report.” Freedom House. [https://freedomhouse.org/country/lesotho/freedom-world/2021](https://freedomhouse.org/country/lesotho/freedom-world/2021) (May 10, 2024).

“Malnutrition Rate by Country 2024.” [https://worldpopulationreview.com/country-rankings/malnutrition-rate-by-country](https://worldpopulationreview.com/country-rankings/malnutrition-rate-by-country)(May 10, 2024).

“Namibia: Freedom in the World 2024 Country Report.” Freedom House. [https://freedomhouse.org/country/namibia/freedom-world/2024](https://freedomhouse.org/country/namibia/freedom-world/2024) (May 10, 2024).

Nkiaka, Elias, Uche T. Okpara, and Murat Okumah. 2021. “Food-Energy-Water Security in Sub-Saharan Africa: Quantitative and Spatial Assessments Using an Indicator-Based Approach.” Environmental Development 40: 100655. doi:[10.1016/j.envdev.2021.100655](https://doi.org/10.1016/j.envdev.2021.100655).

Ottoboni, Kellie, Fraser Lewis, and Luigi Salmaso. 2018. “An Empirical Comparison of Parametric and Permutation Tests for Regression Analysis of Randomized Experiments.” Statistics in Biopharmaceutical Research 10(4): 264–73. doi:[10.1080/19466315.2018.1458648](https://doi.org/10.1080/19466315.2018.1458648).

“Sklearn.Ensemble.RandomForestRegressor.” scikit-learn. [https://scikit-learn/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html](https://scikit-learn/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html) (May 10, 2024).

Slomski, Kathryn. 2023. “Health Care in Sub-Saharan Africa: 21st Century Trends & Forecasts.” D’Amore-McKim School of Business. [https://damore-mckim.northeastern.edu/news/health-care-in-sub-saharan-africa-21st-century/](https://damore-mckim.northeastern.edu/news/health-care-in-sub-saharan-africa-21st-century/)(May 9, 2024).

Team, EPM Information Development. “RMSE (Root Mean Squared Error).” Oracle Help Center. [https://docs.oracle.com/en/cloud/saas/planning-budgeting-cloud/pfusu/insights_metrics_RMSE.html](https://docs.oracle.com/en/cloud/saas/planning-budgeting-cloud/pfusu/insights_metrics_RMSE.html) (May 10, 2024).

“THE 17 GOALS | Sustainable Development.” [https://sdgs.un.org/goals](https://sdgs.un.org/goals) (May 9, 2024).

### Appendix A:
![](https://lh7-us.googleusercontent.com/83NEMpROF91LuPKv9gAwjMQUdxujcVfbX94f-epwRwNfCtlvgEOEnrVhGCPfzEFisc9vBToqGoBAqwvlJmLguKAZl0TorEbc0PCipMuI5wJDVdMlxmAVFmftUSNUrEa_P0iMonVDfvuP2UqyyDyzEpo)

  
![](https://lh7-us.googleusercontent.com/_sf7Ld8ant3JETqtF4gB6ZpOsWc41m6dXK3qsxeWRqPkLcnSY9LsnX72IcwYySENTr0CKuampybFHYRIowJHVubG4n3UxGcxZkiJ3oWp7VznHRw7kQGGLHw923kagafUPJeCXTBocbbBmDoc4HJA_DI)  
![](https://lh7-us.googleusercontent.com/Dp7jxtrczdaG9LEWNXl_wIKTn2l4Umue5obN7l3d1kts65BMGM1VTIV6VYA__QjZ6kYrqc-8PfDI33jGufCetSf7GnG7pajQD0hog5VTqGTMzrDHRg9-QorjXGElV62ZsONzXmm5F18Z6K5xsPin5_E)

--- 

![](https://lh7-us.googleusercontent.com/QhfHc9mOLRtuzVl4gf1T-ZTewQTUvf3QQnY5wK9zds9-lC84IUubXgfTnPh9fnEw9aqySr1yjNtz4D0reWzZX7UVbEMY3lf7cHEJ4bpFxOXqayrgAWfXd0EVehEsMyP6G7enDqxSLFtgz6Y4i6Ydjdk)  
  

![](https://lh7-us.googleusercontent.com/8Kjq3t5mrYfvn317bsHqI1O_vuVExBFmOlyEVV4-A8YWBi4SbhmSAiJbsZpVRFEBspgtXPRfyef0HC6lPn4_301tRgBfKbfLFbzm12jbU3vtNYzrD0TweaX-cZEGAGo0lp8B9gSLFKCY2EG9ELkvrEU)

**![](https://lh7-us.googleusercontent.com/RgScDfPkUWg21WwiYSL2dTF1XzCGtw-EowXxzrio2rVA034qBXX15QPAp3By6Ujf0ZUhAgXpLXsHwpbZVpCoPO4-KRoqy7w7rYKNhQfyEflTBCresrgQU2yzQdViuK8t-Nl7PcDp1PNh_oX60T-TgZA)

### Appendix B:

**![](https://lh7-us.googleusercontent.com/KrhfTOi9KUw061utFCbAm4iptunjzCt20Mrav12XBx55CQwr0vG9oyzyd4W3-9WgqCce8No4HLMVPaN8AoJs2J9amO74lj5IXrNcqz66owd88nLUnCEOdeXCzLwO35BAJvXwo5CybHOztoMHQ8wdogY)**

**![](https://lh7-us.googleusercontent.com/KrhfTOi9KUw061utFCbAm4iptunjzCt20Mrav12XBx55CQwr0vG9oyzyd4W3-9WgqCce8No4HLMVPaN8AoJs2J9amO74lj5IXrNcqz66owd88nLUnCEOdeXCzLwO35BAJvXwo5CybHOztoMHQ8wdogY)**

**![](https://lh7-us.googleusercontent.com/uxwQO5Fuedk1ZFcRd77_QDy3M--iP8xFQhxbRPQdWLPpcoR-gNSdewMau_6-mD5_5vtvKZnI6kXd6aItCIAB7JEHZcCpjjA5L6c67UWvp2CmfxNuefx_wHmhoecIl-yI81zzVsD3aUTEXG3rhQhI5ho)**
