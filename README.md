 <font size = +2><center><u>Predicting Future Demand for the Flu Vaccine</u></center></font>

Authors: [Roshni Janakiraman](mailto:roshnij618@gmail.com)

![needle](/images/1-flushot.jpg)  

# Overview
As one of the leading vaccine distributors in the U.S., AmerisourceBergen relies on accurate predictions of flu vaccine demand. I sought to create a machine learning model to predict seasonal flu vaccine recipients.

Using data from the CDC's National 2009 H1N1 Flu Survey, I trained Tree-Based Models to predict who receives the seasonal flu vaccine, based on demographics, flu vaccine opinions, and flu-conscientious behaviors.

I also illustrate how the current data and models can be used to help AmerisourceBergen with inventory planning (what types of flu shots to offer customers) and marketing (encouraging doctors to promote flu shot recipients).
    
My results and recommendations are presented below.

# Business & Data Understanding

![AB](/images/2-AmerisourceBergen-Logo.jpg)

2022 marked one of the [worst flu seasons](https://www.vox.com/2022/12/6/23494948/flu-influenza-rsv-covid-vaccine-chart-tripledemic-tridemic) in the past 5 years. Broadly available vaccines are crucial to addressing this issue.

As one of the largest medical distributors in America [AmerisourceBergen](https://www.amerisourcebergen.com/insights/physician-practices/supporting-flu-vaccine-access) is committed to making sure that there is an ample supply of seasonal flu vaccines, available to patients whenever and wherever they may need them. AmerisourceBergen prioritizes **empowering customers with increased access to seasonal flu vaccines** through their innovative distribution model, which involves:

1. Ensuring reliable and timely vaccine deliveries to their customers (retail pharmacies, healthcare providers)
2. Forming relationships with multiple vaccine manufacturers & providing insight on market trends
3. Innovating supply chain & logistic management to have the right supply in the right place, at the right time

Each of these objectives is reliant upon *early planning*: accurate prediction of supply & demand is necessary to ensure patients can get vaccinated as early in the flu season, as possible.

Therefore, the current project seeks to identify the *best predictive model* for AmerisourceBergen to use to accurately predict future flu vaccine recipients.

## Project Objectives

The current project seeks to use predictive modeling to accurately identify people who are likely to receive the seasonal flu vaccine in the future, therefore allowing AmerisourceBergen to predict vaccine demand. The following business questions guide this exploration:

1. Based on previous data, can a machine learning model be trained to accurately identify seasonal flu vaccine recipients? 

2. What *types* of seasonal flu vaccines should AmerisourceBergen offer customers? Based on CDC guidelines and population demographics, how much of each type of vaccine should AmerisourceBergen invest in? Using the machine learning model, can we predict how much of each vaccine AmerisourceBergen should have in inventory?

3. How can AmerisourceBergen's relationship with healthcare providers help increase the nationwide vaccination rate?

## Data Source & Relevance to Business Case

The current project uses data from the CDC's [National 2009 H1N1 Flu Survey], which includes phone interview survey data from over 25,000 participants about their seasonal & H1N1 vaccine status, demographics, opinions about the flu vaccine, and flu-conscientious behaviors.

Along with its large size, relevant features, and focus on the seasonal flu, this dataset is especially notable to inform predictions in the recent future. 

This data was collected during the 2009 H1N1 breakout, in a similar health climate as current times due to the co-occurence of a new pandemic (2009: H1N1 | current: COVID-19), along with the seasonal flu epidemic-- a rare occurence that makes this data notable for informing current decisions.

---

# Data Exploration and Business Insights:

The data exploration process provided valuable business insights to inform AmerisourceBergen's marketing and inventory planning efforts. Specifically, I sought to answer the following questions:

1. How can AmerisourceBergen work with healthcare providers to increase the nationwide vaccination rate?
2. What *types* of seasonal flu vaccines should AmerisourceBergen offer its clients? How much of each type is needed?

## 1. Supporting Healthcare Provider Influence on Seasonal Flu Vaccination Rates

![docrec](/images/3-docrec.png)

* People who receive a doctor's recommendation are more likely to get the flu vaccine, whereas those who don't are more likely not to get the flu vaccine

* In total, only 33% of people are recommended to get the vaccine by their doctor
* AmerisourceBergen should continue to advocate for doctors to talk about seasonal flu vaccines during appointments, even when its not flu season

* In addition, AmerisourceBergen can provide marketing information and tools (e.g. promotional brochures, pamphlets, goodies) to doctors to facilitate the recommendation process and build customer goodwill.


## Inventory Planning: Subpopulations, Vaccination Rates, and Types of Seasonal Flu Vaccines

* There are multiple types of flu vaccines [approved by the CDC](https://www.cdc.gov/flu/prevent/different-flu-vaccines.htm), many of which were designed for specific subpopulations.
* It is important to consider population demographics and vaccination likelihood to make sure that the correct supply of these vaccines is provided to these subpopulations

### 2. Flu Vaccines in the Elderly

*The CDC does not recommend a standard flu shot for people above the ages of 65+. The seasonal flu vaccines recommended for the elderly are the *high-dose flu vaccine* and *adjuvanted flu vaccine*

![age](/images/4-age.png)

* The elderly make up the largest group of vaccine recipients: a much larger number of elderly people received the flu vaccine than any other age group.

* The elderly make up 25% of all vaccinated people - a higher percentage than any other age group.

* AmerisourceBergen should prioritize stocking and offering a proportional amount of Fluzone High-Dose Quadrivalent and Fluad Quadrivalent vaccines.


### 3. Flu Vaccines in People with Chronic Illness

* The *recombinant vaccine* creates a stronger immune response, and is therefore recommended for people with weak immune systems.

![chr_ill](/images/5-chr_ill.png)

* Although the number of vaccine recipients with chronic illness is lower than the number of vaccine recipients without a chronic illness, a significant portion of the chronically ill population get the vaccine
* A greater ratio of people with chronic illness are vaccinated compared to people without chronic illness.
* AmerisourceBergen should offer a proportional supply of recombinant vaccines, and focus on marketing these vaccines with healthcare providers.

---
# Data Preparation

Please see my Jupyter Notebook for a full walkthrough on my data preparation process.

## Main Steps
1. Feature Selection
2. Data Cleaning
3. Visualized variable distributions and relationship between the outcome variable (Seasonal Flu Vaccine Received: Yes/No) and predictor variables
4. Calculated Composite Variables for:
    * Flu Conscientiousness Behaviors
    * Pro-Vaccination Opinions
5. Constructed Pre-Processing Pipeline:
    1. Missing Data Imputation using:
        * Mean for Numeric Variables
        * Most Frequent for Categorical Variables
    2. Dummy Creation for Categorical Variables (OneHotEncoder)
    3. Scaling Numeric Variables (StandardScaler)
--- 

# Modeling

I decided to use iterative tree-based models for this project because tree-based models are capable of handling categorical variables, along with large amounts of data (n=26707) and input variables. 

## Metrics of Interest:
### Training Models:
1. Cross-Validation Score
    * To estimate test score accuracy and compare models)
2. Training Score Accuracy
    * To gauge overfitting by comparing with Cross-Validation score

### Final Model:
1. Test Accuracy Score (top priority)
    * For supply and logistic planning, AmerisourceBergen needs a model that will accurately distinguish who will get the vaccine vs. not
2. Recall Score
    * Recall score tells us how accurately the model can predict vaccine demand: out of all of the people who want a vaccine, how many can the model correctly identify?

## Modeling Steps:

1. Dummy Model (Baseline)
2. Decision Tree (First Simple Model)
3. Random Forest Model
4. Grid Search for tuning hyper parameters of Random Forest Model
5. **Tuned Random Forest Model - Final Model**

Below is a table summarizing key statistics from the training models:

|Model|Cross-Validation Score|Overfitting|
|---|---|---|
|Dummy|0.531|--|
|Decision Tree|0.644|High Overfitting|
|First Random Forest|0.756|High Overfitting|
|Final Random Forest|0.764|Reduced Overfitting|


# Final Model Evaluation
### Final Model - Test Metrics
* Test Accuracy: **0.77**
* Recall Score: **0.74**

### Most Important Features 
![features](/images/6-features.png)
   * **Doctor Recommendation** and **Age Group** - noted in Business Insights section
   * **Location** seems to be the most important predictor of vaccine recipients (represented by both Metropolitan Area and US Region)
   * **Education** is also an important factor in determining future vaccine recipients
---

# Conclusions
The final model had:
1. **Test score accuracy** of **77**%
    * The model could accurately distinguish vaccine recipients from non-recipients 77% of the time
2. **Recall score** of **74%** 
    * The model accurately predicted 74% of people who *actually* received the vaccine
    * 74% accuracy in estimating vaccine demand

## Recommendations
* With a 74% recall score, this model has shown that it is capable of predicting future vaccine demand.
* These numbers can be used to estimate supply orders for the 2023 flu season and beyond
* The estimated numbers from this model (y_pred) can also be used to determine the amount of **Elderly & Chronically Ill population** likely to get the vaccine, which can be used to determine **Recombinant** and **High-Dose** flu vaccine orders and demand.

## Limitations
* Model is slightly overfit
    * Model does not perform as well on unseen data as the training data
    * The more that future data deviates from training data, the less accurate the model will be
    * Can be addressed by training model on more (especially recent) data, and reducing features.
    
## Future Directions
1. Include updated, more recent data in model training
2. Obtaining & training model on human-interpretable location metrics
    * Greater exploration of location determinants in predicting flu vaccine recipients is needed
    * Since location was confidential in this dataset, having human interpretable location metrics would allow AmerisourceBergen to derive location-based predictions based on the models' output
        * (e.g. how many people in the Southern part of the United States are likely to get the vaccine?)
        * This will allow AmerisourceBergen to optimize their distribution & shipping routes

---
# For More Information

See the full analysis in the [Jupyter Notebook](./P3-Predicting-Flu-Vaccine-Demand.ipynb) or review this [presentation](./presentation.pdf).

**For additional info, contact Roshni Janakiraman:**<br>
* [Email](mailto:roshnij618@gmail.com) <br>
* [LinkedIn](https://www.linkedin.com/in/roshni-janakiraman/)

![stopflu](/images/7-stoptheflu.jpeg)

## Repository Structure

```
├── scratch_notebooks
│   ├── Scratch.ipynb
│   ├── Rough-Draft.ipynb
│   ├── Final-Draft.ipynb
├── images
│   ├── 1-flushot.jpg
│   ├── 2-AmerisourceBergen-logo.jpeg
│   ├── 3-docrec.png
│   ├── 4-age.png
│   ├── 5-chr_ill.png
│   ├── 6-features.png
│   └── 7-stoptheflu.jpeg
├── Data
│   ├── features.csv
│   ├── labels.csv
├── P3-Predicting-Flu-Vaccine-Demand.ipynb
├── presentation.pdf
└── README.md
```

![stoptheflu](stoptheflu.jpeg)


