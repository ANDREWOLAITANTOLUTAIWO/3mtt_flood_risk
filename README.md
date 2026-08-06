# 3MTT Capstone Project

<img width="209" height="241" alt="3mtt logo2" src="https://github.com/user-attachments/assets/7f69534e-f7cb-4a15-9b2f-692fb1ba7693" />

# Introduction

Riverine communities need flood-risk awareness in order to prepare for and avoid damages caused by flooding. 

This model classifies a community's flood risk from environmental features. Data were captured at 722 locations within the project area. Thus, community members can determine how exposed they are to flood risk by simply imputing their location to the model.  

The model is built around Ero river catchment area. Ero River is in Moba and Ilejemeje LGAs in Ekiti State serving at least seventeen communities with water for irrigation and domestic use. A dam is built on the Ero river at Ikun-Ekiti. But the river causes flooding during raining seasons, and as a result of the operations of the dam.

## Ero River Catchment Area

<img width="764" height="568" alt="ERO_River_Catchment" src="https://github.com/user-attachments/assets/2ed61495-ef98-46a9-ab9a-f581ee3ba8ec" />


## Data Source

In 2025, two PhD candidates, Andrew ToluTaiwo and Thomas Olonisaye, of the University of Lagos did a study on flood susceptibility mapping in Ero River catchment area in Ekiti State, Nigeria. They collected the Flood Predictors dataset used in this project.

## Flood Predictors Used in this Project

Flood Predictors are environmental features, topographic and hydrologic variables, that influence the occurence or magnitude of flooding incidents.  


- **lon: Longitude.** Longitude coordinate of a location

- **lat: Latitude.** Latitude coordinate of a location

- **dist_ri: Distice from River.** Distance in metres from the nearest river

- **elev: Elevation.** Height above mean sea level of the location

- **NDVI: Normalized Difference Vegetation Index.** A measure of occurence of vegetation in the location.

- **NDWI: Normalized Difference Water Index.** A measure of the wetness of the soil.

- **rain: Rainfall.** Amount of rainfall in the region

- **NDBI: Normalized Difference Building Index.** Differentiates between built-up areas and non built-up areas.

- **LULC: Land Use Land Cover.** Land Use refers to how humans use land for various purposes. Land Cover refers to the materials that cover a part of the earth's surface. 0-Water body, 1-Farmland, 2-Forest, 3-Builtup, 4-Bareground

- **rock_por: rock porosity.** Form and porousness of sub-surface rock.

- **rock_perm: Rock Permeability.** Rock permeability affects runoff.

- **Soil_por: Soil Porosity.** Form and porousness of soil.

- **soil_perm: Soil Permeability.** Soil permeability affects runoff.

- **flood_risk: Flood Risk Class.** A location's susceptibility to flooding. This is the target variable. 

# Modeling Procedure

1. Data Exploration
  - Data Cleaning
  - Missing values
  - Investigating feature correlation
  - Data normalization/standardization
2. Training, Validation and Testing Split
3. Model training
4. Cross Validation
5. Model Evaluation
  - Confusion matrix analysis
  - Train/Test accuracy
  - Area under Curve
6. Flood Risk Categories
7. Spatial Distribution of Flood Risk Categories

## Feature Correlation

<img width="835" height="682" alt="Feature_Correlation" src="https://github.com/user-attachments/assets/49898c28-79af-4ea0-a921-26ef765ed136" />

## Data Normalization and Standardization

The sklearn.preprocessing facilitates the transition from 'raw' data to a standard format for algorithm training.

Among such algorithms, we find:

Standardization

Standardization is the first type of transformation to consider, as a large number of machine learning/statistical algorithms assume that the data they operate on is normally distributed. Standardization is expressed as:

𝑥𝑖−mean(𝑥)std(𝑥) 

In practice, the shape of the distribution to work with is ignored and the transformation is simply performed by removing the mean and scaling by the standard deviation.

Note: This is not recommended if the histogram of the target variable is far from Gaussian. In such cases, alternative transformations will be reviewed.

Min-Max Scaling

A good alternative to the previous method is range scaling, which is expressed as:

𝑥𝑖−min(𝑥)max(𝑥)−min(𝑥) 

for  𝑥  being the column to treat, and  𝑥𝑖  the element to transform. This transformation allows the data to range between 0 and 1 and can be used when the distribution of the data does not meet the normality assumption. Note that this transformer is affected by the presence of outliers.

## Logistic Regression
Logistic regression is part of the class of generalized linear models (GLMs), which build directly on top of linear regression. These models take the linear fit and map it through a non-linear function.

Specifically, logistic regression is used when the dependent variable is **binary** (e.g. true/false, yes/no, 0/1) and the goal is to find the relationship between one or more independent variables and the probability of the dependent variable being true or 1.

For logistic regression, the function $f(\cdot)$ is given by $\displaystyle f(z) = \frac{1}{1+\exp(-z)}$ (the *logistic function* - also called the *sigmoid function*).

Where:

- $f(z)$ is the probability of the dependent variable being true or 1
- z is the linear combination of the independent variables and the coefficients of the model:
$\displaystyle z = b_0 + b_1x_1 + b_2x_2 + ... + b_nx_n$

# Results

## Train/Test Accuracy

Train Accuracy: 0.931

Test Accuracy: 0.940

## Confusion Matrix

<img width="683" height="547" alt="Confusion_Matrix_result" src="https://github.com/user-attachments/assets/f5526c34-2a09-4c3e-a59e-77e9d42d68a4" />

From these numbers, we can see that the model is performing quite well, with a higher number of true positives and true negatives. The number of false negatives (4) is lower than false positives (9), which means the model is less likely to miss actual flood-susceptible locations, which is often a critical aspect in flood prediction tasks.

## Area Under Curve

Train AUC: 0.980

Test AUC: 0.987

<img width="567" height="432" alt="AUC_result" src="https://github.com/user-attachments/assets/934c20be-5fd9-473e-8f83-bbdd3d40f2cb" />

## Spatial Distribution of Flood Risk Categories

<img width="1186" height="989" alt="Spatial_Distribution_result" src="https://github.com/user-attachments/assets/42e3173c-1492-472e-9fcd-fe5ba0a90c81" />

This distribution of flood risk categories provides valuable insights into the flood risk of the evaluated locations:

*   **Low Flood-Risk**: These locations have a low probability of flooding, suggesting they are relatively safe. For these areas, standard preventative measures might suffice, and resources can be allocated elsewhere.

*   **Moderate Flood-Risk**: These areas show a noticeable but not extreme probability of flooding. They might require regular monitoring and basic flood preparedness plans. Future development in these areas should consider drainage and infrastructure to mitigate potential risks.

*   **High Flood-Risk**: Locations in this category have a significant chance of experiencing floods. These areas warrant more immediate attention, including early warning systems, robust flood defenses, and strict building codes. Community awareness and evacuation plans are crucial here.

*   **Very High Flood-Risk**: These are the most vulnerable locations, with a very high likelihood of flooding. Urgent and comprehensive flood mitigation strategies are needed, potentially including relocation considerations, major infrastructure projects, and stringent land-use planning. These areas could be prioritized for immediate interventions and resource allocation.

This classification is a powerful tool for urban planners, emergency services, and residents to make informed decisions regarding development, resource allocation, and safety measures in the Ero River catchment area.

# Conclusion

This project successfully developed and evaluated a Logistic Regression model for classifying flood risk in the Ero River catchment area based on various environmental features. By leveraging detailed geospatial and environmental data, the model provides valuable insights into the flood susceptibility of 722 locations.

### Implications:

The generated flood risk map and classifications can serve as a crucial tool for:

*   **Urban Planning**: Informing decisions on new developments and infrastructure projects to minimize exposure to flood hazards.
*   **Emergency Management**: Guiding the deployment of resources, establishment of early warning systems, and planning of evacuation routes.
*   **Community Awareness**: Educating residents about their specific flood risk and promoting preparedness measures.

### Key Takeaways

*   **Logistic Regression is Effective for Flood Risk Classification**: The model demonstrated strong predictive performance (AUC ~0.98), indicating its suitability for this binary classification task.
*   **Importance of Data Preprocessing**: Standardizing the features was crucial for optimal model training and accurate predictions.
*   **Cross-Validation for Robust Evaluation**: K-fold cross-validation provided a more reliable estimate of the model's generalization ability, highlighting both its average performance and variability.
*   **Spatial Analysis is Key for Actionable Insights**: Visualizing flood risk categories on a map transforms model outputs into practical information for stakeholders like urban planners and emergency services.
*   **Feature Importance**: Features like 'dist_ri' (distance from river), 'NDVI', 'elev', 'NDWI', and 'NDBI' were identified as significant predictors, aligning with hydrological understanding of flood susceptibility.
*   **Categorization Aids Decision-Making**: Translating probabilities into distinct risk categories (Low, Moderate, High, Very High) simplifies complex model outputs for non-technical users, facilitating targeted interventions and resource allocation.
