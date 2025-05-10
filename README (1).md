# COVID-19 Vaccination Data Visualization

This project analyzes and visualizes COVID-19 vaccination data using Python. It demonstrates how to clean data, prepare it for analysis, and build an animated bar chart showing the progress of vaccination across countries over time.

## Features

- Data cleaning and preparation using `pandas`
- Animated bar chart using `plotly`
- Visualization of vaccination trends per country over time

## Dataset

A sample vaccination dataset is included in `vaccination_data.csv`. It contains:

- `location`: Country name
- `date`: Date of the data entry
- `people_fully_vaccinated`: Number of fully vaccinated individuals

## Installation

Make sure you have Python installed. Then install the required libraries:

```bash
pip install pandas plotly nbformat ipywidgets
```

> If using Jupyter Notebook, install Jupyter extensions:

```bash
pip install notebook
jupyter nbextension enable --py widgetsnbextension
```

## Usage

1. Open `Extended COVID-19 Vaccination Analysis.ipynb` in Jupyter Notebook or VSCode.
2. Run all cells to:
   - Load the data
   - Clean and prepare it
   - Render the animated bar chart of vaccination progress

## Example Code Snippet

```python
import pandas as pd
import plotly.express as px

df = pd.read_csv("vaccination_data.csv")
df_anim = df.dropna(subset=['people_fully_vaccinated'])
df_anim['people_fully_vaccinated'] = df_anim['people_fully_vaccinated'].astype(float)
df_anim['date_str'] = pd.to_datetime(df_anim['date']).dt.strftime('%Y-%m-%d')

fig = px.bar(
    df_anim,
    x='location',
    y='people_fully_vaccinated',
    color='location',
    animation_frame='date_str',
    title="Vaccination Progress Over Time",
    range_y=[0, df_anim['people_fully_vaccinated'].max() * 1.1]
)
fig.update_layout(xaxis_title="Country", yaxis_title="Fully Vaccinated People")
fig.show()
```

## License

MIT License
