# Exploring-Global-CO-Emissions-and-Renewable-Energy-Trends-1990-2022-
🎯 Objective:
Analyze global CO₂ emissions data and renewable energy adoption to identify patterns, correlations, and trends across countries and over time.
We’ll answer questions like:
Which countries emit the most CO₂?
How have emissions changed over time?
Is there a relationship between renewable energy usage and CO₂ emissions reduction?

🧰 Tools & Libraries:

We’ll use:

pandas       # for data cleaning & analysis
numpy        # for numerical operations
matplotlib   # for visualizations
seaborn      # for advanced plotting
plotly       # for interactive charts (optional)

📂 Dataset:

We can use open datasets from Our World in Data:

CO₂ Emissions dataset

Renewable Energy dataset

Alternatively, you can use Kaggle’s combined dataset:
👉 https://www.kaggle.com/datasets/yoannboyere/co2-ghg-emissionsdata

🧪 Step-by-Step Implementation
1. Import Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

2. Load Data
co2 = pd.read_csv("co2_emissions.csv")
renew = pd.read_csv("renewable_energy.csv")

print(co2.head())
print(renew.head())

3. Data Cleaning

Remove missing values

Filter only relevant columns

Rename for consistency

co2 = co2[['Country', 'Year', 'CO2_emissions']]
renew = renew[['Country', 'Year', 'Renewable_energy_percent']]

# Drop missing values
co2.dropna(inplace=True)
renew.dropna(inplace=True)

4. Merge Datasets
df = pd.merge(co2, renew, on=['Country', 'Year'], how='inner')
print(df.head())

5. Exploratory Data Analysis (EDA)
5.1 Top 10 Emitters in 2022
top_emitters = df[df['Year'] == 2022].nlargest(10, 'CO2_emissions')

plt.figure(figsize=(10,6))
sns.barplot(x='CO2_emissions', y='Country', data=top_emitters, palette='Reds_r')
plt.title("Top 10 CO₂ Emitting Countries in 2022")
plt.xlabel("CO₂ Emissions (million tonnes)")
plt.ylabel("Country")
plt.show()

5.2 Global CO₂ Trend
global_trend = df.groupby('Year')['CO2_emissions'].sum().reset_index()

plt.figure(figsize=(10,5))
sns.lineplot(x='Year', y='CO2_emissions', data=global_trend, color='blue')
plt.title("Global CO₂ Emissions Trend (1990–2022)")
plt.xlabel("Year")
plt.ylabel("Total CO₂ Emissions")
plt.show()

6. Correlation Analysis
corr = df[['CO2_emissions', 'Renewable_energy_percent']].corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.title("Correlation between CO₂ Emissions and Renewable Energy")
plt.show()

7. Country Focus Example
kenya = df[df['Country'] == 'Kenya']

plt.figure(figsize=(10,5))
sns.lineplot(x='Year', y='CO2_emissions', data=kenya, label='CO₂ Emissions')
sns.lineplot(x='Year', y='Renewable_energy_percent', data=kenya, label='Renewables (%)')
plt.title("Kenya: CO₂ Emissions vs Renewable Energy (1990–2022)")
plt.legend()
plt.show()

8. Insights & Conclusions

From the analysis, we might observe:

Global CO₂ emissions peaked in the 2010s but began flattening recently.

Countries investing heavily in renewables (e.g., Germany, Denmark) show slower emissions growth.

Developing economies’ emissions are rising as energy demand increases.

9. Optional: Interactive Dashboard

You can extend this with:

Plotly Dash or Streamlit to create an interactive dashboard:

pip install streamlit
streamlit run app.py


This allows users to select a country and view trends dynamically.

🧾 Deliverables

✅ Clean Jupyter Notebook (co2_renewable_analysis.ipynb)
✅ Visualizations & insights
✅ (Optional) Streamlit Dashboard
