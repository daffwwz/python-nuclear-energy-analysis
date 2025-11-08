# Nuclear Energy Overview Dataset Analytics Project
## Project Overview
Nuclear energy is one of the most reliable and cleanest source of energy that plays a big role in energy transition and climate change mitigation. Public perception, policy decisions, and operational constraints may contribute to the dynamics of its utilization over time despite of its capability to have high capacity factor, means that nuclear energy having a high ratio of actual electricity generated to the maximum possible electricity the plant could have produced if it had operated at full power continuously. This project analyzes this data in order to expose trends and other insights in the nuclear energy sector.

## Tools Used
**1. Python:** Pandas, Matplotlib, Seaborn, Data Wrangler Extension for VS Code

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

## Findings
### Net Summer Capacity of Nuclear Energy
This timeseries data explain the maximum output of nuclear generating units during peak summer conditions. This data basically tells us **how much reliable generation** we can count on during **peak demand periods** (usually in summer).
![alt text](images/net_summer_capacity.png)

