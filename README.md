# Monthly rent and noise exposure of the population of the city of Barcelona: Analysis and dimensionality reduction
Task for the hackathon within Jump2digital 16017 Nov 2023.

## Objective
Reduce the dimensionality of the combined dataset containing data on average monthly rent and population noise exposure in the city of Barcelona through Principal Component Analysis (PCA).

## 1. Introduction
Analysis conducted in this study focuses on rental prices (["Average monthly rent of the city of Barcelona"](https://opendata-ajuntament.barcelona.cat/data/en/dataset/est-mercat-immobiliari-lloguer-mitja-mensual/resource/0a71a12d-55fa-4a76-b816-4ee55f84d327)) and the percentages of the population exposed to different noise levels (["Exposed population to the noise levels from Strategic Noise Map of the city of Barcelona"](https://opendata-ajuntament.barcelona.cat/data/en/dataset/poblacio-exposada-mapa-estrategic-soroll/resource/3846500e-72aa-4780-967f-f09aa184eaba)) in the city of Barcelona.  
Data for both rental prices and noise exposure were collected for 73 neighborhoods within 10 districts in Barcelona. For rental prices, data covered the four quarters of 2017, including the average total rental price and rental price per m2. Noise exposure data covered the period from 2012 to 2017, including 26 "types of noise" and 10 noise levels.
Merged dataset included variables: `Quarter`, `District_code`, `District_name`, `Neighbourhood_code`, `Neighbourhood_name`, `Price`, `Price_m2`, `Area`, and all columns related to the percentages of the population exposed to various types and levels of noise.

## 2. Data Preprocessing
- Addressed missing values by removing rows with missing price information. As the target variable was determined to be the rental price per square meter, we could not fill missing values.
- Created a new feature, 'Area,' based on the total price and price per square meter.
- Excluded aggregate indicators (DEN) from noise exposure data, as in some cases, they seemed to have strange values (equal to zero when their components were not zero).
- Expanded noise level ranges to 5 categories instead of the initial 10, as the level of detail regarding noise ranges appears to be very granular. 
- Restructured the noise exposure dataset from a long format to a wide format.
- Eliminated columns where the percentage of the population exposed to specific noise levels was consistently zero in all neighborhoods.
- Excluded from the PCA features were:
  - `District_name` and `Neighbourhood_name` as they have numerical analogs.
  - `District_code` as the rental price was more influenced by the neighborhood rather than the district.
  - Substituted the `Price` variable with the `Area` variable, as rental price per square meter was chosen as the target variable.

## 3. Results
### EDA Insights
- Significant variation in rental prices among neighborhoods in general and among neighborhoods within the same district, with Sarrià-Sant Gervasi being the most expensive district and Nou Barris the least expensive.
- Influence of the quarter on rental prices (e.g. increase in the 3rd quarter during the peak tourist season). For some neighborhoods, the price difference between quarters can be much more pronounced than for others.
- High noise levels exceeding 50 dB in Barcelona, with no neighborhood having noise levels below 40 dB during nighttime for the majority of the population.
- Different neighborhoods experiencing varying levels of noise pollution, with road traffic noise being the predominant source. Noise from industries and railways had a relatively low impact on the population.
- No direct and clear relationship between rental prices and noise levels in neighborhoods.
### PCA Results
- The first 9 principal components retained 80% of the total variance, and the first 17 principal components retained 95% of the total variance.
- The main factors influencing the principal components included percentages of population exposed to road traffic noises, pedestrian and recreational noises, and the absence of noise from railways and industries.
- Transformed dataset with 17 features instead of the original 80 was obtained. This dataset represented the data in a lower-dimensional space using the first 17 principal components obtained through PCA.

## 4. Conclusions
The analysis provides valuable insights into the relationship between rental prices and noise exposure in Barcelona, and the PCA was conducted to reduce dimensionality and create a more efficient feature space. The main factors influencing the principal components were related to noise exposure, particularly road traffic and pedestrian/recreational noises. Potential actions for future analysis include focusing on aggregated noise exposure indicators, considering specific noise types, and exploring non-linear relationships between features, as no direct and clear relationship between rental prices and noise levels in neighborhoods was seen.
