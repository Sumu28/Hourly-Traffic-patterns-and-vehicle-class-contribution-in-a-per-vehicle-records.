## License
This project is licensed under the MIT License. The dataset is sourced from Transport Infrastructure Ireland and is subject to their data usage terms.

## Overview 
This project analyzes hourly traffic patterns using large-scale per-vehicle sensor data from Transport Infrastructure Ireland (TII). The goal is to identify the busiest hour of the day and determine which vehicle classes contribute most to peak traffic using exploratory and explanatory visualizations.

## Research Question
At which hour of the day is traffic highest, and which vehicle class contributes most to that peak?

## Dataset
Source: Transport Infrastructure Ireland (TII)
Data type: Per-vehicle traffic sensor records
Size: ~700MB, ~4.7 million rows, 26 columns
Coverage: Single day (2013-06-01)
Link: https://data.tii.ie/traffic-counter-readme.html
The dataset represents real-time inductive loop traffic sensor detections and is suitable for demonstrating large-scale data cleaning and visualization techniques.

## Data Processing & Cleaning

Skipped corrupted rows during parsing of the raw CSV file
Standardized column names
Mapped numeric vehicle class codes to human-readable labels (Car, Van/LGV, HGV, etc.)
Constructed timestamps from separate time components
Removed invalid timestamps and unmapped vehicle classes
Aggregated traffic counts by hour and vehicle class

## Visualization

Exploratory charts:
Vehicle-class distribution
Total hourly traffic volume

## Final visualization:

Multi-line hourly traffic chart
Separate lines for each vehicle class
Bold line representing total traffic

The final chart clearly highlights peak traffic hours and dominant vehicle types.

## Tools & Libraries Used

Python
Pandas, NumPy
Plotly
Jupyter Notebook
Google Colab (for large-file processing)

## Key Findings

Traffic peaks in the late afternoon
Cars are the dominant contributors to peak traffic
Vans/LGVs are the second largest contributors
Heavy Goods Vehicles show more stable patterns throughout the day
