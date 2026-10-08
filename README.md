# When Is Irish Traffic Busiest, and Who Is Driving It?

**Hourly traffic patterns and vehicle-class contributions from 4.7 million individual vehicle records**

Roadside sensors on Ireland's roads record every vehicle that passes. That produces a huge amount of data, and the useful question is a simple one: **at what hour is traffic at its highest, and which type of vehicle is responsible for the peak?**

This project takes one full day of raw per-vehicle detections from Transport Infrastructure Ireland (TII), cleans it up, and answers that question with a single chart.

> Group project for a Data Visualisation module at Dublin City University, done with **Kavya Kumar**. *(Add the module code if you want to name it.)*

---

## Results

**The short answer:** traffic peaks at **12:00 (noon)**, and **cars** drive that peak.

*(Add your final chart image here. It is the most useful thing in this README.)*

### When is traffic busiest?

Traffic is at its lowest in the small hours, climbs steeply through the morning, peaks at noon, then eases off slowly through the afternoon and evening.

| Hour | Vehicle detections |
|---|---|
| 00:00 | 60,677 |
| 01:00 | 38,685 |
| 02:00 | 27,831 |
| 03:00 | 26,486 (quietest of the hours above) |
| 04:00 | 33,118 |
| **12:00** | **398,415 (peak)** |

From the final chart, traffic stays high through the afternoon, still around 300,000 an hour at 18:00, before dropping to roughly 75,000 by 23:00. *(These afternoon and evening figures are read from the chart, so replace them with exact values from the notebook if you want precision.)*

### Who is driving it?

Ranked by total detections across the day:

1. Car
2. Van / LGV
3. Articulated HGV
4. Rigid HGV
5. Motorcycle
6. Multi-Axle HGV
7. Bus / Minibus
8. Unclassified

- **Cars dominate everything.** They make up the large majority of detections, and they are the largest class at the noon peak. Vans and light goods vehicles come second, well behind.
- **Heavy goods vehicles barely move.** Their lines stay almost flat while total traffic swings by hundreds of thousands, so they are not what causes the peak.
- **Heavy vehicles matter more at night.** At midnight, cars made up 51,572 of the 60,677 detections (about 85%), and the three HGV classes together made up about 7%. Their share is highest when everything else is quiet.

The takeaway: the daily peak is caused by ordinary private cars, with light commercial vehicles second, and not by freight.

## The data

- **Source:** [Transport Infrastructure Ireland traffic counter data](https://data.tii.ie/traffic-counter-readme.html), per-vehicle records for **1 June 2013** ([direct file](https://data.tii.ie/Datasets/TrafficCountData/2013/06/01/per-vehicle-records-2013-06-01.csv)).
- **Size:** about 710 MB, **4,769,072 rows and 26 columns**, recorded by roadside inductive loop counters.
- **Why one day, and why 2013?** TII releases single sample days of this data. It is old, but it is real sensor data at a scale that makes cleaning and visualisation a proper exercise.

The file is too large to store here, so it is not included. Download it from the link above.

## What I did with it

1. **Loading it.** The file had malformed lines that broke the standard CSV reader. I loaded it with Python's parsing engine and skipped the bad lines, so only the corrupted rows were lost and the rest stayed usable.
2. **Tidying the columns.** I lower-cased the column names and dropped three columns that were not needed (`axleweights`, `straddlelanename` and `axlespacings`, the last of which was empty).
3. **Naming the vehicle types.** Vehicles came as numeric class codes, so I mapped them to readable names: Motorcycle, Car, Van / LGV, Bus / Minibus, Rigid HGV, Articulated HGV, Multi-Axle HGV and Unclassified.
4. **Building timestamps.** Time was split across separate year, month, day, hour, minute and second columns, so I combined them into a proper datetime. Rows with impossible values would have been set aside rather than guessed at.
5. **Counting.** I grouped detections by hour and vehicle class, then pivoted them into one table with a total for each hour.
6. **Charting.** Two exploratory charts first (detections per class, and total traffic by hour), then the final multi-line chart.

**Why a multi-line chart?** We tried a stacked bar chart first, but it makes the smaller classes hard to compare across hours. A line for each vehicle class, plus a bold line for the total, shows both the overall peak and who contributes to it. We sketched both options by hand before building anything.

## Things worth knowing

- **It is one Saturday.** 1 June 2013 was a Saturday, so this is weekend traffic. A midday peak fits that kind of day. A weekday would probably show morning and evening rush-hour peaks instead, so the result should not be read as typical for every day.
- **Counts add up all counter sites.** The data covers many roadside counters, and I counted detections across all of them. The chart shows total detections on the network, not the traffic on one road.
- **Class names rely on the TII class scheme.** I mapped codes 0 to 7 using the UK/Ireland inductive loop classes used by TII. *(Check this against TII's own documentation before relying on the names.)*
- **Cars dominate the whole dataset.** Cars far outnumber every other class, which is why the smaller classes sit near the bottom of the chart. That imbalance shaped the choice of a line chart.

## If we had more time

- Compare several days, including weekdays and weekends
- Break it down by lane or by individual counter site
- Add an animation over the day (we tried, but it was too heavy for a dataset this size)

---

## Tech stack

Python · Pandas · NumPy · Plotly · Matplotlib · Jupyter Notebook · Google Colab

## Run it yourself

```bash
git clone https://github.com/Sumu28/<your-repo-name>.git
cd <your-repo-name>
pip install pandas numpy plotly matplotlib jupyter
```

Download the dataset from the link above, then open `DataVisualization_final.ipynb`. The notebook reads a file named `per-vehicle-records-2013-06-01(1).csv`, so either rename your download to match or change the file name in the loading cell.

## Repository contents


```
DataVisualization_final.ipynb     # cleaning, analysis and charts
Hourly_Traffic_patterns_and_vehicle.pdf   # the written report
README.md
```

## Who did what

Sumukha Sagar loaded the 700 MB dataset and sorted out the parsing problems. We both cleaned the data in Colab, mapped the vehicle classes, built the timestamps and made the exploratory charts. We chose the final chart and its design together, and Kavya Kumar built the final polished version.

## Authors

Sumukha Sagar and Kavya Kumar
School of Computing, Dublin City University
