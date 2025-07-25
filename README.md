# 🚕 Uber_Fares_Dataset_Analysis_PowerBI_Project.

## 📌 Personal Introduction.

**Names:** Irakoze Grace Vanny  
**ID:** 26425

**Group:** E

**Course:** Introduction to Big Data Analytic-INSY 8413

## 📌 Introduction.

This project analyzes the Uber Fares Dataset using Python and Power BI to explore fare trends, ride durations, time-based patterns, and more. The goal is to create a clean, interactive dashboard that can help stakeholders understand key operational metrics of Uber ride activity.

---

## 📌 Project Overview

- **Dataset Source:** [Uber Fares Dataset - Kaggle](https://www.kaggle.com/datasets/yasserh/uber-fares-dataset) 
- **Tools Used:** Python (Pandas), Power BI Desktop
- **Objective:** Gain insights into fare patterns, time trends, and ride behaviors using data analysis and visual storytelling.
- **My Kaggle worksheet:** https://www.kaggle.com/code/irakozevannygrace/introduction-to-big-data-analytic-kaggle


## 🔍 Project Phases

### 1. Data Understanding & Preparation
- Loaded raw data using Pandas
- Assessed data quality, types and structure
- Cleaned dataset (handled missing values, outliers and format issues)

### 2. Exploratory Data Analysis (EDA)
- Visualized fare distribution
- Analyzed correlations between fare amount, distance, and time
- Detected outliers and patterns

### 3. Feature Engineering
- Extracted hour, day, month from timestamps
- Categorized peak vs. off-peak hours
- Encoded new categorical variables

### 4. Power BI Visualization
- Imported enhanced dataset
- Designed time-series and geographic visuals
- Highlighted busiest periods and seasonal variations

---

## 🖼️ All Results Images

> 📷 Below are the screenshots and visual evidences of various stages of my project:

1. **Data Cleaning Process**

```python

# Check for missing values
print(df.isnull().sum())

# Drop rows with missing key values
df.dropna(subset=['pickup_datetime', 'pickup_latitude', 'pickup_longitude',
                  'dropoff_latitude', 'dropoff_longitude', 'fare_amount'], inplace=True)

# Remove rows with invalid fare amounts
df = df[(df['fare_amount'] > 0) & (df['fare_amount'] < 1000)]

# Filter latitude and longitude (NYC bounds as rough check)
df = df[(df['pickup_latitude'].between(40, 42)) & 
        (df['pickup_longitude'].between(-75, -72)) &
        (df['dropoff_latitude'].between(40, 42)) &
        (df['dropoff_longitude'].between(-75, -72))]

print("Shape after cleaning:", df.shape)

```
   
<img width="960" height="504" alt="image" src="https://github.com/user-attachments/assets/56f701b5-a91a-4893-a734-bc1f4479797a" />

**. Output**

<img width="959" height="503" alt="image" src="https://github.com/user-attachments/assets/5746a11e-a60e-40d5-83a2-d28ea712d78c" />


2. **Exploratory Analysis**

```python

from geopy.distance import geodesic

# Convert pickup_datetime to datetime
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'])

# Extract temporal features
df['hour'] = df['pickup_datetime'].dt.hour
df['day'] = df['pickup_datetime'].dt.day
df['month'] = df['pickup_datetime'].dt.month
df['weekday'] = df['pickup_datetime'].dt.day_name()
df['year'] = df['pickup_datetime'].dt.year

# Peak hours (7-9 AM or 5-7 PM)
df['is_peak'] = df['hour'].apply(lambda x: 1 if 7 <= x <= 9 or 17 <= x <= 19 else 0)

# Calculate distance (in km)
def calculate_distance(row):
    pickup = (row['pickup_latitude'], row['pickup_longitude'])
    dropoff = (row['dropoff_latitude'], row['dropoff_longitude'])
    return geodesic(pickup, dropoff).km

df['distance_km'] = df.apply(calculate_distance, axis=1)

print(df[['fare_amount', 'hour', 'weekday', 'is_peak', 'distance_km']].head())

```

<img width="547" height="335" alt="image" src="https://github.com/user-attachments/assets/10c44309-2039-4f06-a298-e9d7b1f89990" />

<img width="539" height="248" alt="image" src="https://github.com/user-attachments/assets/6933961b-635d-4542-89da-1885a5577fe0" />

**output**

<img width="960" height="504" alt="image" src="https://github.com/user-attachments/assets/82c32aab-3a77-481d-8020-7babc0bae0f3" />

3. **Dashboard Building using Power BI**

📊 1. Fare Distribution

Insight: Understand how most fares are distributed (e.g., most below $20)

📊 2. Fare vs Distance

Insight: Are longer rides always more expensive? Any anomalies?

📊 3. Fare vs Time of Day

Insight: Identify expensive hours of the day (e.g., peak hours)

📊 4. Rides by Day of Week

Insight: See ride trends across the week

📊 5. Monthly Ride Trends

Insight: Understand seasonal patterns

📊 6. Peak vs Off-Peak Analysis

Insight: Compare demand and fare between peak and non-peak hours

📊 7. Map of Pickup Locations

Insight: Identify popular pickup zones

---

## 📊 Final Project Dashboard

**My Interactive Power BI dashboard** showcasing the final analysis and insights:

👉 <img width="960" height="503" alt="image" src="https://github.com/user-attachments/assets/c6941f76-0765-4c0b-8130-a1502dec256c" />

---

## 📧 Contact

For any questions or feedback, feel free to contact:

**IRAKOZE Grace Vanny**  
📩 vannygrace2020@gmail.com

---

## 🛡️ Integrity Consideration

This project is my original work and follows all academic honesty guidelines as stated. All scripts, insights, and visuals are my own contributions.

Thank You...
---
