# Nuclear Energy Overview Dataset Analytics and Forecasting Project
## Project Overview
Nuclear energy is one of the most reliable and cleanest source of energy that plays a big role in energy transition and climate change mitigation. Public perception, policy decisions, and operational constraints may contribute to the dynamics of its utilization over time despite of its capability to have high capacity factor, means that nuclear energy having a high ratio of actual electricity generated to the maximum possible electricity the plant could have produced if it had operated at full power continuously. This project analyzes this data in order to expose trends and other insights in the nuclear energy sector.

## Tools Used
**Python:** Pandas, Matplotlib, Seaborn, Data Wrangler Extension for VS Code, Sci-kit Learn, XGBoost

## Dataset Source
**Kaggle**:	[Nuclear Energy Datasets](https://www.kaggle.com/datasets/alistairking/nuclear-energy-datasets)
### Data Structure (The description's copied from the Kaggle ReadME file)
| Column Name | Description | Datatype |
| --- | --- | --- |
| `Year` | The year for the data entry. | Integer |
| `Month` | The month for the data entry. | Object |
| `Nuclear Generating Units, Total Operable Units` | The total number of operable nuclear generating units (data not always available). | Object |
| `Nuclear Generating Units, Net Summer Capacity` | The net summer capacity of nuclear generating units in million kilowatts. | Float |
| `Nuclear Electricity Net Generation` | The net generation of electricity from nuclear power in millions of kilowatt-hours. | Integer |
| `Nuclear Share of Electricity Net Generation` | The percentage share of total electricity net generation coming from nuclear power. | Float |
| `Nuclear Generating Units, Capacity Factor` | The capacity factor (actual output vs potential output) of nuclear generating units. | Float |

## Result Summary

## Data Cleaning
Removed the `Nuclear Generating Units, Total Operable Units` column because of too many missing data `Not Available`.

## Forecasting Method
1. The method used for the time series forecasting is by using `XGBoost` model to predict the `Nuclear Electricity Net Generation` as the target value. The feature added for the forecasting are `lag_7`, `rolling_mean_1`, `rolling_std_1`, `rolling_mean_7`, `rolling_std_7`, `rolling_mean_30`, `rolling_std_30`, `Month`, `Year`, `Quarter`, `DayOfWeek`, and `DayOfYear`. 
2. The target value is also scaled using `StandardScaler` from `Sci-kit Learn` module before training.
3. The dataframe is splitted using `TimeSeriesSplit` as a cross validation method.
4. The Hyperparameter tuning uses `GridSearchCV` method and found the best parameter for the model: {'learning_rate': 0.01, 'max_depth': 2, 'n_estimators': 2000}.

## Findings
### Data Statistics Summary
| index   |   Nuclear Generating Units, Net Summer Capacity |   Nuclear Electricity Net Generation |   Nuclear Share of Electricity Net Generation |   Nuclear Generating Units, Capacity Factor |
|---------|-------------------------------------------------|--------------------------------------|-----------------------------------------------|---------------------------------------------|
| count   |                                        614      |                                614   |                                     614       |                                    614      |
| mean    |                                         85.6071 |                              49806.5 |                                      17.2166  |                                     76.4963 |
| std     |                                         23.2862 |                              19647.1 |                                       4.17584 |                                     16.2811 |
| min     |                                         14.533  |                               5697   |                                       3.9     |                                     34.6    |
| 25%     |                                         78.7078 |                              31481.5 |                                      15.525   |                                     61.025  |
| 50%     |                                         98.533  |                              57362   |                                      18.8     |                                     79.15   |
| 75%     |                                         99.628  |                              65169.2 |                                      20.1     |                                     91.875  |
| max     |                                        102.206  |                              74649   |                                      22.9     |                                    101.6    |

### Correlation Heatmap
![alt text](images/correlation_heatmap.png)

### Net Summer Capacity of Nuclear Energy
This timeseries data explains the maximum output of nuclear generating units during peak summer conditions. This data basically tells us **how much reliable generation** we can count on during **peak demand periods** (usually in summer). The line plot shows an overall increase in the net capacity of nuclear power, primarily during **the Major Expansion Era (1973–1990)** (highlighted in green), when the number of operating plants rose from 109 to 413. In the subsequent period from 1990 to 2003, there were **59 new plants commissioned and 50 plants shut down**, indicating a **slowdown in growth** caused by **the Three Mile Island (1979)** and **the Chernobyl Accident (1986)**. The most recent five-year data also shows a **decline in net capacity**, reflected by a **total annual growth rate of –3.74%** [[1](https://www.oecd.org/en/publications/forty-years-of-uranium-resources-production-and-demand-in-perspective_9789264028074-en.html)].

![alt text](images/net_summer_capacity_annotated.png)

### Nuclear Electricity Net Generation
The data show a clear upward trend in the total electricity generated by nuclear power plants (NPPs). This increase reflects the growing role of nuclear energy in meeting global electricity demand, supported by improvements in reactor performance and operational efficiency. 
![alt text](images/nuclear_electricity_net_generation.png)

### Nuclear Share of Electricity and Nuclear Capacity Factor
The Nuclear Share of Electricity and the Nuclear Capacity Factor both show how much nuclear power contributes to overall electricity generation, and they often move in the same direction. The Nuclear Share of Electricity tells us what percentage of total electricity comes from nuclear energy relative to all energy source, while the Capacity Factor shows how much of a plant’s full potential is being used.
![alt text](images/nuclear_share_n_capacity_factor.png)

### Seasonality Impact on Nuclear Electricity Net Generation and Capacity Factor
This plot shows how the total electricity generated by nuclear energy and the capacity factor vary by month. The data indicate that nuclear electricity generation and capacity factor peak during the **summer** and **winter** seasons, when electricity demand is high due to the use of air conditioners in summer and heaters in winter. Meanwhile, they reach their lowest levels in spring and autumn, when electricity demand is relatively lower, making these seasons the ideal time for scheduled maintenance outages at nuclear power plants.
![alt text](images/nuclear_electricity_net_generation_seasonal.png)
![alt text](images/nuclear_capacity_factor_seasonal.png)

# Net Electricity Generation Forecasting

## References
[[1](https://www.oecd.org/en/publications/forty-years-of-uranium-resources-production-and-demand-in-perspective_9789264028074-en.html)] OECD Nuclear Energy Agency (NEA) & International Atomic Energy Agency (IAEA). Forty Years of Uranium Resources, Production and Demand in Perspective: The Red Book Retrospective. OECD Publishing, 2006.
