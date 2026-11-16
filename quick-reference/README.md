# Python Quick Reference Guide

Practical Python for geographical data analysis using Google Colab, NumPy, Pandas, GeoPandas, Xarray and Matplotlib, including loops, conditionals and automation.

This guide supports **GY674: Earth Science Data Analysis in Python** and **GY675: Visualising Inequality** at Maynooth University. It is also intended as a useful starting point for postgraduate researchers and staff who are new to Python.

> **How to use this guide:** You do not need to memorise Python syntax. Use this guide when you know what you want to do but cannot remember exactly how to write it. The weekly notebooks provide the structured route through the course; this guide is here when you need a reminder.

The guide contains material from across the whole module, so **you are not expected to understand every section immediately**. Start with the sections introduced in class and return to the others as the course progresses.

---

## Contents

1. [Google Colab, Python and Jupyter notebooks](#1-google-colab-python-and-jupyter-notebooks)
2. [Importing packages](#2-importing-packages)
3. [Python fundamentals](#3-python-fundamentals)
4. [NumPy arrays](#4-numpy-arrays)
5. [Pandas and tabular data](#5-pandas-and-tabular-data)
6. [Dates and time series](#6-dates-and-time-series)
7. [Vector data and GeoPandas](#7-vector-data-and-geopandas)
8. [Xarray and multidimensional data](#8-xarray-and-multidimensional-data)
9. [Data visualisation](#9-data-visualisation)
10. [Errors and debugging](#10-errors-and-debugging)
11. [Reproducible notebooks and GitHub](#11-reproducible-notebooks-and-github)
12. [Using generative AI responsibly](#12-using-generative-ai-responsibly)
13. [Learning resources and documentation](#13-learning-resources-and-documentation)

---

# 1. Google Colab, Python and Jupyter notebooks

## What is Python?

**Python** is a programming language.

Packages such as NumPy, Pandas, Xarray and Matplotlib extend Python with tools for numerical computing, data analysis and visualisation.

## What is a Jupyter notebook?

A **Jupyter notebook** is an interactive document that combines:

- executable Python code;
- results and error messages;
- tables and figures;
- headings, explanations and links written in Markdown.

Notebook files use the extension `.ipynb`.

## What is Google Colab?

**Google Colab** is Google's online environment for opening and running Jupyter notebooks.

It provides Python and many common packages through a web browser, so no local Python installation is required.

The relationship is:

> **Python** is the language → **Jupyter notebook** is the document → **Google Colab** is the online environment we use to work with it.

## Code cells and text cells

A notebook contains different types of cells:

- **Code cells** contain Python code.
- **Text cells** contain headings, explanations and instructions written in Markdown.
- **Output** appears beneath a code cell after it runs.

Useful shortcuts:

- **Shift + Enter** — run a cell and move to the next cell.
- **Ctrl + Enter** or **Cmd + Enter** — run a cell and stay in the current cell.

Try this in a code cell:

```python
print("Hello from Python")
```

## Comments

Anything after `#` is a **comment**.

```python
temperature = 15  # Daily temperature in °C
```

Python ignores comments when running the code. They are notes for the person reading it.

## Writing in a text cell

Text cells use **Markdown**:

```markdown
# Main heading

## Smaller heading

### Even smaller heading

**bold text**

*italic text*

- first item
- second item
```

Use text cells to explain what you are doing rather than creating a notebook containing unexplained code.

## The runtime

The **runtime** is the temporary computer session that executes your Python code.

Variables, temporary files and packages installed during the session may be lost when the runtime restarts or disconnects.

Your saved notebook remains available, but you may need to rerun its cells.

> **Remember:** The notebook is the saved document; the runtime is the temporary computer running it.

## A reliable Colab workflow

1. Open the course notebook and save your own copy.
2. Connect to the runtime.
3. Work through the notebook from top to bottom.
4. Run cells as you go.
5. Look at the output after each step.
6. Read error messages when something does not work.
7. Before submitting work, restart the runtime and run all cells from top to bottom.

> **Common problem:** If Python says a variable does not exist, check whether you have run the cell that creates it.

## Accessing files in Colab

Small files can be uploaded using the **Files** panel on the left of Colab.

These files are temporary and disappear when the runtime is reset.

To access files stored in Google Drive:

```python
from google.colab import drive

drive.mount("/content/drive")
```

A file in Drive can then be opened using its path, for example:

```python
file_path = "/content/drive/MyDrive/data/test_data.csv"

df = pd.read_csv(file_path)
```

Only mount Drive in notebooks you trust, because code in the notebook can access files available through the mounted Drive.

---

# 2. Importing packages

Python can be extended using **packages**.

We import a package when we want to use the tools it provides.

Common packages used in this module are:

```python
import numpy as np
import pandas as pd
import geopandas as gpd
import rasterio
import xarray as xr
import matplotlib.pyplot as plt
```

These names and aliases are standard conventions:

| Package | Short name | Used for |
|---|---|---|
| NumPy | `np` | Numerical arrays and calculations |
| Pandas | `pd` | Tabular data |
| GeoPandas | `gpd` | Vector spatial data (points, lines and polygons) |
| Rasterio | `rasterio` | Raster spatial data (e.g. GeoTIFF elevation grids) |
| Xarray | `xr` | Multidimensional Earth science data |
| Matplotlib | `plt` | Data visualisation |

For example:

```python
import numpy as np
```

means:

- `import` — load a package;
- `numpy` — the package name;
- `as np` — use the shorter name `np` in our code.

We can then use NumPy tools such as:

```python
np.array([10, 12, 14])
```

> **Tip:** Package imports are normally kept together near the beginning of a notebook.

Avoid importing everything from a package:

```python
# Avoid this
from numpy import *
```

Explicit package names make code easier to understand.

---

# 3. Python fundamentals

## Variables

A **variable** gives a piece of information a name so that we can store it and use it again.

```python
temperature = 15
```

Here:

- `temperature` is the variable name;
- `=` assigns a value;
- `15` is the value stored in the variable.

Variables can store different kinds of information:

```python
station = "Maynooth"
temperature = 15
rainfall = 12.5
is_raining = True
```

Use meaningful variable names:

```python
annual_temperature = 11.2
```

Python is case-sensitive:

```python
temperature
Temperature
```

These are treated as different names.

## Basic data types

Some common Python data types are:

| Type | Meaning | Example |
|---|---|---|
| `int` | Whole number | `15` |
| `float` | Decimal number | `12.5` |
| `str` | Text | `"Maynooth"` |
| `bool` | True or False | `True` |

Use `type()` to check what kind of information a variable contains:

```python
temperature = 15

type(temperature)
```

returns:

```text
int
```

Python treats numbers and text differently:

```python
rainfall = 12.5
```

is a number, while:

```python
rainfall = "12.5"
```

is text.

## Displaying results

Entering a variable at the end of a code cell displays its value:

```python
temperature
```

You can also use `print()`:

```python
print(temperature)
```

`print()` is particularly useful when you want to display several results:

```python
print("Temperature:", temperature)
print("Rainfall:", rainfall)
```

## Basic calculations

Python can be used like a calculator:

```python
10 + 5
10 - 5
10 * 5
10 / 5
```

Variables can be used in calculations:

```python
rainfall_day_1 = 12.5
rainfall_day_2 = 8.2

total_rainfall = rainfall_day_1 + rainfall_day_2
```

## Lists

A **list** stores multiple values together in one variable.

```python
rainfall = [12.5, 8.2, 10.9, 5.2, 30.1]
```

Lists use **square brackets `[]`**, with values separated by commas.

Lists can also contain text:

```python
stations = ["Maynooth", "Donegal", "Dublin"]
```

Use `len()` to find the number of values:

```python
len(rainfall)
```

## Indexing

**Indexing** allows us to access an individual value.

Python starts counting at **0**, not 1.

```python
rainfall = [12.5, 8.2, 10.9, 5.2, 30.1]

rainfall[0]   # first value
rainfall[1]   # second value
rainfall[2]   # third value
```

The final value can be selected using:

```python
rainfall[-1]
```

Values in a list can also be changed:

```python
rainfall[0] = 15.0
```

## Slicing

**Slicing** allows us to select multiple values.

The basic pattern is:

```python
data[start:stop]
```

For example:

```python
rainfall[1:4]
```

selects the values at positions `1`, `2` and `3`.

> **Important:** The `stop` position is **not included**.

Think of `start` and `stop` as boundaries around the values you want to select.

Useful patterns include:

```python
rainfall[0:3]   # first three values
rainfall[:3]    # first three values
rainfall[2:]    # third value onwards
rainfall[-3:]   # final three values
```

A useful rule is:

> **stop - start = number of values selected**

For example:

```python
rainfall[1:4]
```

selects:

```text
4 - 1 = 3 values
```

## Other Python collections

You will encounter other ways of storing information later:

```python
coordinates = (53.38, -6.59)

station_info = {
    "name": "Maynooth",
    "elevation": 48
}
```

- A **tuple** is an ordered collection often used for values that belong together.
- A **dictionary** stores information using named keys.

For example:

```python
station_info["name"]
```

returns:

```text
Maynooth
```

## Operators and comparisons

Python can compare values:

```python
temperature > 20
temperature < 20
temperature == 20
temperature != 20
temperature >= 20
temperature <= 20
```

Common operators are:

| Operator | Meaning |
|---|---|
| `=` | Assign a value |
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

Conditions can be combined:

```python
is_valid = (temperature > -50) and (temperature < 60)
```

Pandas filters use `&`, `|` and `~` instead, as shown later.

## Conditions, loops and automation

Loops and conditionals allow us to **repeat operations and make decisions automatically**, particularly when analysing several datasets.

### For loops

A `for` loop repeats an operation for each item in a sequence:

```python
stations = ["Athens", "Dublin", "Madrid"]

for station in stations:
    print(station)
```

The variable `station` takes a new value each time through the loop. The colon `:` starts the loop, and **indentation** identifies the code that is repeated.

### Using `range()`

Use `range()` to work through a sequence of numbers:

```python
for year in range(2020, 2025):
    print(year)
```

This prints 2020 through 2024. **The stop value is not included.** `range(10)` represents 0 through 9; use `list(range(10))` to display those values together.

### `if`, `elif` and `else`

Conditions allow Python to choose which code to run:

```python
temperature = 20

if temperature >= 30:
    print("Hot day")
elif temperature >= 15:
    print("Mild day")
else:
    print("Cold day")
```

Python checks conditions **in order**. Only the first matching branch runs; `else` runs if none match.

### Combine a loop and a conditional

```python
temperatures = [12, 18, 25, 31, 9]

for temp in temperatures:
    if temp >= 30:
        print(temp, "Hot day")
    else:
        print(temp, "Not a hot day")
```

Notice the **two levels of indentation**: the conditional sits inside the loop, and its actions sit inside the conditional.

### F-strings and changing filenames

An **f-string** inserts a variable's value into text using curly brackets `{}`:

```python
city = "Dublin"
filename = f"era5_{city}_daily.csv"
print(filename)  # era5_Dublin_daily.csv
```

This is useful for filenames, plot titles and messages that change on each iteration.

### Automate checks across CSV files

```python
import pandas as pd

cities = ["Athens", "Bergen", "Dublin", "Helsinki", "Madrid"]

# data_dir is the folder containing the CSV files
for city in cities:
    filename = f"era5_{city}_daily.csv"
    df = pd.read_csv(data_dir + filename)

    missing = df["precipitation_mm"].isna().sum()

    if missing > 0:
        print(f"{city}: {missing} missing precipitation values")
    else:
        print(f"{city}: No missing precipitation values")
```

Here, `data_dir` must already be defined as the path to the folder, ending with `/`. The loop reads each dataset, and the conditional reports whether any precipitation values are missing.

> **Key idea:** A loop repeats an analysis; a conditional makes decisions; together they let us automate workflows across many datasets. Code **inside** a loop runs on each iteration; code **after** the loop runs once.

## Functions, methods and attributes

You will encounter several slightly different ways of asking Python to do something:

```python
print(temperature)          # function

df["temperature"].mean()    # method

df.shape                    # attribute

pd.read_csv("data.csv")     # function from a package
```

You do not need to memorise these terms immediately.

A useful pattern to recognise is:

```python
object.method()
```

For example:

```python
df["temperature"].mean()
```

means: calculate the mean of the `temperature` column in a DataFrame.

## Defining a simple function

A function packages an operation so that it can be reused:

```python
def kelvin_to_celsius(temperature_k):
    temperature_c = temperature_k - 273.15
    return temperature_c
```

Use it with:

```python
kelvin_to_celsius(291.55)
```

which returns:

```text
18.4
```

---

# 4. NumPy arrays

NumPy stands for **Numerical Python**.

It provides tools for working efficiently with numerical data.

Its main data structure is the **array**.

## Why use a NumPy array?

A Python list can store several values:

```python
temperature = [10, 12, 14, 16, 18]
```

But numerical calculations with lists do not always behave as you might expect.

For example:

```python
temperature * 2
```

repeats the list:

```text
[10, 12, 14, 16, 18, 10, 12, 14, 16, 18]
```

A NumPy array behaves differently:

```python
import numpy as np

temperature = np.array([10, 12, 14, 16, 18])

temperature * 2
```

returns:

```text
[20 24 28 32 36]
```

The calculation is applied to **every value in the array**.

This makes NumPy arrays very useful for numerical data analysis.

## Create an array

Convert a list into a NumPy array:

```python
temperature = [10, 12, 14, 16, 18]

temperature = np.array(temperature)
```

Or create the array directly:

```python
temperature = np.array([10, 12, 14, 16, 18])
```

## Calculate with an array

Operations are applied across the values:

```python
temperature + 2
temperature - 5
temperature * 2
temperature / 2
```

## Select values

NumPy arrays use the same basic indexing and slicing that you have already learned:

```python
temperature[0]      # first value

temperature[-1]     # final value

temperature[0:3]    # first three values

temperature[:3]     # first three values

temperature[2:]     # third value onwards
```

## Calculate summary statistics

Useful methods include:

```python
temperature.mean()   # mean

temperature.min()    # minimum

temperature.max()    # maximum

temperature.sum()    # total
```

You can combine slicing and calculations:

```python
temperature[:3].mean()
```

This first selects the first three values and then calculates their mean.

## Inspect an array

As you progress through the module, these can help you understand an array:

```python
temperature.shape   # size of each dimension

temperature.dtype   # data type stored in the array

temperature.ndim    # number of dimensions

temperature.size    # total number of values
```

> **Common mistake:** Python lists and NumPy arrays can look very similar but behave differently during calculations. Use `type()` if you are unsure what you are working with.

---

# 5. Pandas and tabular data

Pandas is used for **tabular data** organised into rows and columns.

A **DataFrame** contains rows and columns. A single column is usually a **Series**.

## Read a CSV file

```python
import pandas as pd

df = pd.read_csv("data.csv")
```

Replace `"data.csv"` with the name or path of your own file.

## Inspect a dataset

Before analysing a new dataset, look at what it contains:

```python
df.head()      # first 5 rows

df.tail()      # final 5 rows

df.info()      # columns, data types and missing values

df.describe()  # summary statistics

df.shape       # number of rows and columns

df.columns     # column names

df.dtypes      # data type of each column
```

## Select columns

Select one column:

```python
df["temperature"]
```

Select several columns:

```python
df[["date", "temperature"]]
```

## Select rows and columns

Use `.loc` to select using labels:

```python
df.loc[0:4, ["date", "temperature"]]
```

Use `.iloc` to select using numerical positions:

```python
df.iloc[0:5, 0:2]
```

`.iloc` uses the same stop-before-the-final-position slicing pattern introduced earlier.

## Filter observations

For example, keep observations where temperature is greater than 20°C:

```python
warm = df[df["temperature"] > 20]
```

Combine conditions using `&`:

```python
wet_and_warm = df[
    (df["precipitation"] > 0) &
    (df["temperature"] > 20)
]
```

For Pandas filters:

- `&` means **and**
- `|` means **or**
- `~` means **not**

Put individual comparisons inside parentheses.

## Filter using a list of values

To select observations belonging to any of several categories, use `.isin()`:

```python
selected = df[df["region"].isin(["Leinster", "Munster"])]
```

## Sort observations

Sort a DataFrame by a column:

```python
sorted_df = df.sort_values("temperature")            # lowest to highest
sorted_df = df.sort_values("temperature", ascending=False)  # highest to lowest
```

To sort a Series of calculated results, use `.sort_values()` without a column name:

```python
mean_by_region = df.groupby("region")["temperature"].mean()
mean_by_region.sort_values()
```

## Missing values

Count missing values:

```python
df.isna().sum()
```

Remove rows containing missing values:

```python
df_complete = df.dropna()
```

Replace missing temperatures with the mean:

```python
df["temperature"] = df["temperature"].fillna(
    df["temperature"].mean()
)
```

These are different approaches. The correct treatment depends on what the missing values represent.

> **Scientific check:** Never remove or replace missing observations without understanding and explaining the decision.

## Group and summarise

Calculate a mean for different groups:

```python
df.groupby("region")["income"].mean()
```

More detailed summaries can be created using:

```python
summary = (
    df.groupby("region")
      .agg(
          mean_income=("income", "mean"),
          population=("population", "sum")
      )
      .reset_index()
)
```

## Save a table

```python
df.to_csv("analysis_results.csv", index=False)
```

---

# 6. Dates and time series

Dates should normally be stored as dates rather than ordinary text.

## Convert dates

```python
df["date"] = pd.to_datetime(df["date"])
```

If dates use a known format, specify it explicitly. For example, for day/month/year dates:

```python
df["date"] = pd.to_datetime(df["date"], format="%d/%m/%Y")
```

Use dates as the DataFrame index:

```python
df = df.set_index("date")
```

## Select dates

```python
df.loc["2020"]
```

selects observations in 2020.

```python
df.loc["2020-01":"2020-12"]
```

selects January to December 2020.

## Aggregate time series

Calculate monthly mean temperature:

```python
monthly_temperature = df["temperature"].resample("MS").mean()
```

Calculate annual mean temperature:

```python
annual_temperature = df["temperature"].resample("YS").mean()
```

Calculate annual precipitation totals:

```python
annual_precipitation = df["precipitation"].resample("YS").sum()
```

Calculate a 30-row moving mean:

```python
rolling_temperature = df["temperature"].rolling(30).mean()
```

> **Scientific check:** Match the calculation to the variable. Temperature is often averaged, while precipitation amounts may be summed. Always check what the original variable represents.

---

# 7. Vector data and GeoPandas

**GeoPandas** extends Pandas to work with vector data: **points, lines and polygons**. A **GeoDataFrame** is like a DataFrame, but includes a `geometry` column describing geographical features.

## Read and inspect vector data

```python
import geopandas as gpd

ed_gdf = gpd.read_file("electoral_divisions.gpkg")  # GeoPackage
# gpd.read_file("boundaries.shp")                    # Shapefile

ed_gdf.head()       # preview attributes and geometry
ed_gdf.columns      # column names
ed_gdf.shape        # rows and columns
ed_gdf.plot()       # quick map
```

Most Pandas operations, including filtering, `.isna()` and `.merge()`, also work with GeoDataFrames.

## Check and transform the CRS

A **Coordinate Reference System (CRS)** defines how coordinates relate to locations on Earth.

```python
ed_gdf.crs                                # inspect CRS
ed_gdf = ed_gdf.to_crs("EPSG:2157")       # transform to Irish Transverse Mercator
```

- `EPSG:2157` — Irish Transverse Mercator (ITM); Eastings/Northings in metres.
- `EPSG:4326` — WGS 84; longitude/latitude in degrees.

**Remember:** `.to_crs()` transforms coordinates; `.set_crs()` assigns a CRS without transforming them. Match CRSs before combining spatial layers.

## Join attributes to polygons

```python
pobal_df = pd.read_csv("pobal.csv", dtype={"ED_ID_STR": str})
pobal_df["ED_ID_STR"] = pobal_df["ED_ID_STR"].str.zfill(6)

ed_deprivation_gdf = ed_gdf.merge(
    pobal_df, on="ED_ID_STR", how="left"
)

ed_deprivation_gdf.isna().sum()  # check missing values after joining
```

A left merge retains all ED boundaries. Check that identifiers match, including leading zeros.

## Map and summarise polygons

```python
# Choropleth: colour polygons by a numerical attribute
ed_deprivation_gdf.plot(
    column="Deprivation_score", cmap="RdBu", legend=True
)

# Dissolve EDs into counties and calculate mean ED score
mean_depriv_county = ed_deprivation_gdf.dissolve(
    by="COUNTY", aggfunc={"Deprivation_score": "mean"}
)
```

`cmap` selects a Matplotlib colormap. `.dissolve()` combines polygons by category and aggregates attributes. Here the county mean is **unweighted across EDs**, not a population-weighted deprivation score.

## Combine map layers and save

```python
fig, ax = plt.subplots(figsize=(8, 9))

mean_depriv_county.plot(ax=ax, color="lightgrey", zorder=1)
rail_gdf.to_crs(mean_depriv_county.crs).plot(
    ax=ax, color="darkgreen", zorder=2
)
stations_gdf.to_crs(mean_depriv_county.crs).plot(
    ax=ax, color="red", markersize=20, zorder=3
)

ax.set_axis_off()
fig.savefig("map.png", dpi=300, bbox_inches="tight")
plt.show()
```

`zorder` controls which layers appear on top. For interactive maps, try `ed_gdf.explore()` (requires the optional interactive-mapping dependencies).

> **Key idea:** GeoPandas combines familiar Pandas-style tables with geometry, coordinate systems and spatial mapping.

---

# 8. Xarray and multidimensional data

Xarray is particularly useful for **labelled multidimensional Earth-system data**, including ERA5 gridded climate data stored in **netCDF (`.nc`)** files. Unlike a simple table, a gridded dataset can vary across **time, latitude and longitude**.

## Open an ERA5 netCDF dataset

```python
import xarray as xr

ds = xr.open_dataset("era5_temperature.nc")
```

Replace the example filename with the path to your own file. `ds` is an Xarray **Dataset**, which can contain multiple variables.

## Explore the dataset

```python
ds                 # overview of the dataset
ds.data_vars       # available variables
ds.dims            # dimensions and their sizes
ds.coords          # coordinate labels
ds.attrs           # dataset metadata
```

An Xarray **DataArray** is one labelled variable; a **Dataset** groups related variables. Typical ERA5 coordinates are `time`, `latitude` and `longitude`, but always inspect the file rather than assuming its structure.

## Select ERA5 temperature and convert units

ERA5 2-metre air temperature is commonly stored as `t2m` in **kelvin (K)**:

```python
temperature_k = ds["t2m"]
temperature_c = temperature_k - 273.15
```

Check the variable's attributes and units before converting:

```python
ds["t2m"].attrs
```

## Select dates and locations with `.sel()`

Select one date (or timestamp present in your dataset):

```python
one_day = temperature_c.sel(time="2022-08-01")
```

Select a period:

```python
period = temperature_c.sel(time=slice("2001", "2020"))
```

Select the grid cell nearest to Maynooth:

```python
maynooth = temperature_c.sel(
    latitude=53.38,
    longitude=-6.59,
    method="nearest"
)
```

Select a geographical area (check coordinate order first):

```python
ireland = temperature_c.sel(
    latitude=slice(55.5, 51.0),
    longitude=slice(-11.0, -5.0)
)
```

> **Remember:** `.sel()` uses coordinate **labels** (such as dates and latitude/longitude), not integer positions. Latitude may increase or decrease depending on the dataset; inspect `ds.latitude` before slicing.

## Calculate averages across dimensions

The dimension named in `.mean(dim=...)` is the one you **average over**.

Average through time to produce a map of mean temperature:

```python
mean_map = temperature_c.mean(dim="time")
```

Average over latitude and longitude to produce a time series of spatial mean temperature:

```python
spatial_mean = temperature_c.mean(dim=["latitude", "longitude"])
```

Calculate annual means of that spatial-mean time series:

```python
annual_mean = spatial_mean.resample(time="YS").mean()
```

**Scientific check:** This is an unweighted mean of grid cells. For a physically representative regional or global area mean on a latitude–longitude grid, grid-cell area weighting may be required.

## Create a map and a time-series plot

Xarray has convenient built-in plotting methods using Matplotlib:

```python
import matplotlib.pyplot as plt

# Temperature map for one date
one_day.plot()
plt.title("ERA5 2-metre temperature (°C)")
plt.show()
```

```python
# Annual spatial-mean temperature time series
annual_mean.plot()
plt.title("Annual mean ERA5 temperature")
plt.ylabel("Temperature (°C)")
plt.show()
```

## Calculate a climatology and anomalies

For a dataset covering the reference period, calculate a **1991–2020 mean temperature at each grid cell**:

```python
baseline = temperature_c.sel(time=slice("1991", "2020"))
climatology = baseline.mean(dim="time")
```

Subtract the climatology to obtain temperature departures from that reference mean:

```python
anomalies = temperature_c - climatology
```

This is a **single 1991–2020 mean for each grid cell**, not a separate seasonal or day-of-year climatology. Only use the 1991–2020 baseline if your dataset actually covers that period.

## Inspect before calculating

```python
temperature_c.dims
temperature_c.shape
temperature_c.coords
temperature_c.attrs
```

Common climate unit conversions:

```python
temperature_c = temperature_k - 273.15  # K to °C
precipitation_mm = precipitation_m * 1000  # m to mm
```

> **Key idea from Lab 6:** **Read → Explore → Select → Analyse → Visualise.** Xarray lets you work with 3D gridded climate data using familiar labels and operations. Always check dimensions, units, spatial coverage and the period of record before interpreting results.

---

# 9. Data visualisation

A good figure should communicate the data clearly.

The chart type and accurate representation of the data matter more than decoration.

## A basic line graph

A common Matplotlib pattern is:

```python
import matplotlib.pyplot as plt

day = ["Mon", "Tue", "Wed", "Thu", "Fri"]
temperature = [10, 12, 14, 13, 16]

fig, ax = plt.subplots(figsize=(7, 4))

ax.plot(day, temperature, marker="o")

ax.set(
    title="Daily temperature",
    xlabel="Day",
    ylabel="Temperature (°C)"
)

plt.show()
```

You do not need to memorise all of this immediately.

A useful way to think about it is:

```python
fig, ax = plt.subplots()
```

creates the figure and a plotting area.

Then:

```python
ax.plot(...)
```

draws data on that plotting area.

Finally:

```python
plt.show()
```

displays the completed figure.

## Plot a time series from a DataFrame

Later in the module, you might plot data directly from Pandas:

```python
fig, ax = plt.subplots(figsize=(9, 5))

ax.plot(
    df.index,
    df["temperature"],
    linewidth=1.5
)

ax.set(
    title="Annual temperature at Maynooth",
    xlabel="Year",
    ylabel="Temperature (°C)"
)

ax.grid(alpha=0.25)

plt.tight_layout()
plt.show()
```

## Experiment with a figure

One of the best ways to learn Matplotlib is to change something and rerun the cell.

For example:

```python
fig, ax = plt.subplots(figsize=(10, 4))
```

changes the figure size.

You can experiment with the marker:

```python
ax.plot(day, temperature, marker="s")
```

or line style:

```python
ax.plot(day, temperature, marker="o", linestyle="--")
```

> **Tip:** Change one thing at a time, rerun the cell and look at what happens.

## Compare distributions and relationships

A **histogram** shows how values are distributed:

```python
fig, ax = plt.subplots(figsize=(7, 4))
ax.hist(df["temperature"], bins=15)
ax.set(xlabel="Temperature (°C)", ylabel="Number of observations")
plt.show()
```

A **boxplot** can compare the distributions of two groups:

```python
fig, ax = plt.subplots(figsize=(7, 4))
ax.boxplot([group_a, group_b], tick_labels=["Group A", "Group B"])
ax.set(ylabel="Value")
plt.show()
```

Here, `group_a` and `group_b` are collections of numerical values that you have selected.

A **scatter plot** helps explore the relationship between two numerical variables:

```python
fig, ax = plt.subplots(figsize=(7, 4))
ax.scatter(df["temperature"], df["precipitation"], alpha=0.5)
ax.set(xlabel="Temperature (°C)", ylabel="Precipitation (mm)")
plt.show()
```

Look for overall patterns, clusters and unusual observations. A visible relationship does **not** necessarily mean that one variable causes the other.

## Plot spatial Xarray data

```python
fig, ax = plt.subplots(figsize=(8, 6))

temperature.mean(dim="time").plot(
    ax=ax,
    cmap="RdBu_r",
    cbar_kwargs={"label": "Temperature (°C)"}
)

ax.set_title("Mean annual temperature, 2001–2020")

plt.show()
```

## Save a figure

```python
fig.savefig(
    "figure.png",
    dpi=300,
    bbox_inches="tight"
)
```

Here:

- `"figure.png"` is the output filename;
- `dpi=300` produces a high-resolution raster image;
- `bbox_inches="tight"` removes unnecessary surrounding whitespace.

## Figure checklist

Before considering a figure finished, ask:

- Is the variable clear?
- Are the units clear?
- Is the location and time period clear where relevant?
- Is the chart type appropriate for the data?
- Is the title informative?
- Are the axis labels readable?
- Can the figure be understood without reading the code?
- Is the data source identified where appropriate?
- Are colours and labels accessible and readable?

---

# 10. Errors and debugging

Errors are a normal part of programming.

An error does not mean that you have failed. It means Python has encountered something it cannot execute.

Read the error message rather than immediately rerunning the same code.

## Common errors

| Error | Likely meaning |
|---|---|
| `NameError` | A variable or package has not been defined |
| `IndexError` | You requested a position that does not exist |
| `KeyError` | A requested column or label does not exist |
| `FileNotFoundError` | Python cannot find the file |
| `TypeError` | An operation was applied to an unsuitable type of object |
| `ValueError` | The type may be acceptable, but the value or format is unsuitable |
| `SyntaxError` | Python cannot understand how the code has been written |

## A simple debugging sequence

When something does not work:

**1. Read the error.**

Look particularly at the final line.

**2. Find the line of your code that caused the problem.**

**3. Check simple things first.**

- Is the variable name spelled correctly?
- Did you run the earlier cell?
- Are quotation marks or brackets missing?
- Are you using the correct index?
- Did you import the package?

**4. Inspect what you are working with.**

For example:

```python
type(data)
```

or later in the course:

```python
df.head()
df.shape
temperature.dims
```

**5. Change one thing and run the code again.**

> **Good programming practice:** Do not be afraid to experiment. Change something, run the cell, inspect the result and learn from what happens.

---

# 11. Reproducible notebooks and GitHub

A reproducible notebook should allow another person — or your future self — to understand what you did and recreate the analysis.

A **repository** is a project folder tracked by GitHub.

A **commit** is a saved checkpoint with a short message explaining what changed.

GitHub stores the notebook and its history; Colab provides the environment in which the notebook runs.

## Notebook checklist

A good notebook should:

- have a clear title;
- explain the purpose of the analysis;
- identify the data source, variables and units;
- keep package imports together near the beginning;
- use meaningful variable names;
- separate stages using Markdown headings;
- include relevant data-quality checks;
- explain important analytical decisions;
- run successfully from top to bottom;
- remove unused or failed experimental code before submission.

Before finishing:

> **Restart the runtime and run every cell from top to bottom.**

Do not commit passwords, API keys, personal data or restricted datasets to GitHub.

> **Remember:** Reproducibility is not simply code that runs. The data, assumptions, transformations and interpretation must also be clear.

---

# 12. Using generative AI responsibly

Generative AI can support learning and professional data analysis, but it can also hide gaps in understanding.

You remain responsible for every line of code and every result in your notebook.

> **Important:** **Generative AI is not permitted for Assignment 1 in GY674/GY675**, including generating or debugging code and writing interpretations. The general guidance below is for learning activities where AI use is permitted; assessment-specific rules always take precedence.

## Appropriate learning uses

Generative AI can help you:

- explain an error message in plain language;
- request a hint after you have attempted a problem;
- explain what an existing line of code does;
- compare two possible approaches;
- suggest ways to check a result;
- review code that you have already attempted.

## Uses that do not demonstrate learning

Be cautious about:

- pasting an assessment task into an AI tool;
- accepting a complete generated workflow;
- repeatedly generating code until something runs;
- using functions or methods that you cannot explain;
- assuming code is scientifically correct simply because it executes.

## Recommended learning sequence

> **Attempt → Run → Inspect → Think → Get a hint if needed → Modify → Run again → Verify**

The aim is not simply to produce working code. The aim is to understand what the code is doing and whether the result makes sense.

---

# 13. Learning resources and documentation

The weekly course notebooks provide the main structured route through the course.

The resources below provide additional explanations, examples and documentation when you need them.

## Recommended course textbook

### [Introduction to Python for Geographic Data Analysis](https://pythongis.org/)

**Tenkanen, Heikinheimo and Whipp (2025)**

This is the recommended free online textbook supporting the weekly laboratory notebooks.

Selected sections will be signposted during the course. You are **not expected to read or complete the entire book**.

> **Reference:** Tenkanen, H., Heikinheimo, V. and Whipp, D. (2025) *Introduction to Python for Geographic Data Analysis* [e-book]. Available at: https://pythongis.org/

## Additional learning resources

### Project Pythia Foundations

https://foundations.projectpythia.org/

Project Pythia provides open tutorials for Python-based computing in the geosciences, including:

- NumPy;
- Pandas;
- dates and calendars;
- Matplotlib;
- NetCDF and Xarray;
- Cartopy;
- Git and GitHub.

> **Best suited to:** students who want to extend the material introduced in class.

### Python for Data Analysis — Wes McKinney

https://wesmckinney.com/book/

A detailed open-access resource for Pandas and general data-analysis workflows.

> **Best suited to:** students and researchers who expect to use Pandas extensively.

## Official documentation

You are not expected to read package documentation from beginning to end.

Use it when you need to look up a particular method, function or example.

### Python and Google Colab

- Python tutorial: https://docs.python.org/3/tutorial/
- Google Colab FAQ: https://research.google.com/colaboratory/faq.html

### NumPy

- NumPy documentation: https://numpy.org/doc/stable/
- NumPy quickstart: https://numpy.org/doc/stable/user/quickstart.html

### Pandas

- Pandas user guide: https://pandas.pydata.org/pandas-docs/stable/user_guide/
- 10 minutes to Pandas: https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html
- Pandas cheat sheet: https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf
- Pandas for spreadsheet users: https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_spreadsheets.html
- Pandas for R users: https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_r.html

### Matplotlib

- Matplotlib documentation: https://matplotlib.org/stable/
- Matplotlib cheat sheets: https://matplotlib.org/cheatsheets/

### GeoPandas

- GeoPandas documentation: https://geopandas.org/en/stable/
- Getting started with GeoPandas: https://geopandas.org/en/stable/getting_started/introduction.html
- GeoPandas user guide: https://geopandas.org/en/stable/docs/user_guide.html
- Mapping and plotting: https://geopandas.org/en/stable/docs/user_guide/mapping.html
- Merging data: https://geopandas.org/en/stable/docs/user_guide/mergingdata.html
- Coordinate reference systems: https://geopandas.org/en/stable/docs/user_guide/projections.html
- Dissolving geometries: https://geopandas.org/en/stable/docs/user_guide/aggregation_with_dissolve.html

### Xarray

- Xarray documentation: https://docs.xarray.dev/en/stable/
- Xarray in 45 minutes: https://tutorial.xarray.dev/overview/xarray-in-45-min.html

---

# About this guide

This is a **living reference** and will develop alongside the course.

The weekly notebooks are the main route through the module. Use this guide when you need to **remember syntax, revisit something introduced in class, or find out where to look next**.

Corrections and suggestions are welcome.

Maintained by **Shaun Harrigan**, ICARUS Climate Research Centre, Department of Geography, Maynooth University.
