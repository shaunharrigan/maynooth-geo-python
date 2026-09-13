# Python Quick Reference Guide

Practical Python for geographical data analysis using Google Colab, NumPy, Pandas, Xarray and Matplotlib.

This guide supports **GY674: Earth Science Data Analysis in Python** and **GY675: Visualising Inequality** at Maynooth University. It is also intended as a useful starting point for postgraduate researchers and staff who are new to Python.

> **How to use this guide:** This is a complete reference, available from the beginning of the course. You are not expected to understand every section immediately. Use it to recall methods already introduced, find reliable documentation and identify what you need to learn next. The weekly notebooks provide the structured route through the course.

## Contents

1. [Google Colab, Python and Jupyter notebooks](#1-google-colab-python-and-jupyter-notebooks)
2. [Import conventions](#2-import-conventions)
3. [Python fundamentals](#3-python-fundamentals)
4. [NumPy arrays](#4-numpy-arrays)
5. [Pandas and tabular data](#5-pandas-and-tabular-data)
6. [Dates and time series](#6-dates-and-time-series)
7. [Xarray and multidimensional data](#7-xarray-and-multidimensional-data)
8. [Data visualisation](#8-data-visualisation)
9. [Errors and debugging](#9-errors-and-debugging)
10. [Reproducible notebooks and GitHub](#10-reproducible-notebooks-and-github)
11. [Using generative AI responsibly](#11-using-generative-ai-responsibly)
12. [Learning resources and documentation](#12-learning-resources-and-documentation)

---

## 1. Google Colab, Python and Jupyter notebooks

### What is Python?

**Python** is a programming language. NumPy, Pandas, Xarray and Matplotlib are packages that extend Python for numerical computing, data analysis and visualisation.

### What is a Jupyter notebook?

A **Jupyter notebook** is an interactive document that combines:

- executable Python code;
- results and error messages;
- tables and figures;
- headings, explanations and links written in Markdown.

Notebook files use the extension `.ipynb`.

### What is Google Colab?

**Google Colab** is Google's online environment for opening and running Jupyter notebooks. It provides Python and many common packages through a web browser, so no local Python installation is required.

The relationship is:

> **Python** is the language → **Jupyter notebook** is the document format → **Google Colab** is the online service used to open and run the notebook.

### Opening Google Colab

You can open Colab in several ways:

1. Go to [colab.research.google.com](https://colab.research.google.com/).
2. Sign in with a Google account.
3. Choose a notebook from Google Drive, upload an `.ipynb` file, or open a notebook from GitHub.
4. To create a new notebook, select **File → New notebook**.

When opening a shared course notebook, save an editable copy using **File → Save a copy in Drive**. Do not work directly in the course master copy.

### Code cells, text cells and output

- **Code cells** contain Python commands.
- **Text cells** contain Markdown explanations, headings, links and instructions.
- **Output** appears beneath a code cell after it runs.
- **Shift + Enter** runs a cell and moves to the next cell.
- **Ctrl + Enter** or **Cmd + Enter** runs a cell without moving.

### The runtime

The **runtime** is the temporary remote computer session that executes the Python code. Variables, uploaded files and installed packages held only in the runtime are lost when it restarts or disconnects.

> **Remember:** The notebook is the saved document; the runtime is the temporary computer running it.

### Reliable Colab workflow

1. Open the course notebook and save your own copy.
2. Connect to the runtime.
3. Run the import and data-loading cells first.
4. Work through the notebook from top to bottom.
5. Read outputs and error messages rather than repeatedly pressing Run.
6. Save important data and outputs to persistent storage.
7. Before submission, restart the runtime and run all cells from top to bottom.

> **Common problem:** If Python says a variable does not exist, check whether the cell that creates it has been run in the current runtime.

---

## 2. Import conventions

The Python community uses standard abbreviations for widely used packages:

```python
import numpy as np
import pandas as pd
import xarray as xr
import matplotlib.pyplot as plt
```

The statement `import numpy as np` means that NumPy is available using the shorter name `np`. Therefore, `np.arange()` refers to the `arange` function in NumPy.

Avoid importing every name from a large package:

```python
# Avoid this
from numpy import *
```

Explicit package names make code easier to read and reduce conflicts between functions with similar names.

---

## 3. Python fundamentals

### Variables and basic types

```python
station = "Maynooth"     # str: text
temperature = 18.4       # float: decimal number
year = 2026               # int: whole number
is_wet = True             # bool: True or False

type(temperature)
print(temperature)
```

Python is case-sensitive: `temperature` and `Temperature` are different names.

### Collections

```python
stations = ["Maynooth", "Dublin", "Derry"]        # list
coordinates = (53.38, -6.59)                        # tuple
station_info = {"name": "Maynooth", "elevation": 48}  # dictionary
```

Python starts counting at zero:

```python
stations[0]       # first item
stations[-1]      # final item
stations[0:2]     # first two items; final position is excluded
```

### Operators and comparisons

```python
temperature_c = temperature_k - 273.15
is_warm = temperature_c > 20
is_valid = (temperature_c > -50) & (temperature_c < 60)
```

- `=` assigns a value.
- `==` tests whether values are equal.
- `!=` means not equal.
- `>`, `<`, `>=` and `<=` compare values.

### Conditions and loops

```python
if temperature > 20:
    print("Warm")
else:
    print("Not warm")
```

```python
for station in stations:
    print(station)
```

Indentation is part of Python syntax.

### Functions, methods and attributes

```python
print(temperature)          # function
df.head()                   # method
df.shape                    # attribute
pd.read_csv("data.csv")    # function from Pandas
```

Parentheses call a function or method. Attributes such as `.shape` describe an object and do not use parentheses.

---

## 4. NumPy arrays

NumPy (**Numerical Python**) provides arrays and numerical operations. An array stores data in one or more dimensions. A one-dimensional array resembles a list; a two-dimensional array resembles a table or grid.

### Create and inspect an array

```python
values = np.array([12.1, 14.5, 13.8])

values.shape
values.dtype
values.ndim
values.size
```

### Select values

```python
values[0]             # first value
values[-1]            # final value
values[0:2]           # first two values
values[values > 13]   # values satisfying a condition
```

### Calculate summaries

```python
values.mean()
values.min()
values.max()
values.sum()
np.median(values)
np.std(values)
```

> **Common mistake:** Python lists and NumPy arrays can look similar but behave differently during calculations. Use `type()` when uncertain.

---

## 5. Pandas and tabular data

Pandas is used for labelled tabular data. A **DataFrame** contains rows and columns; a single column is usually a **Series**.

### Read and inspect a CSV file

```python
df = pd.read_csv("data.csv")

df.head()
df.tail()
df.info()
df.describe()
df.shape
df.columns
df.dtypes
```

### Select columns and rows

```python
df["temperature"]
df[["date", "temperature"]]

df.loc[0:4, ["date", "temperature"]]  # label-based
df.iloc[0:5, 0:2]                     # position-based
```

Selecting one column normally returns a Series. Selecting a list of columns returns a DataFrame.

### Filter observations

```python
warm = df[df["temperature"] > 20]

wet_and_warm = df[
    (df["precipitation"] > 0) &
    (df["temperature"] > 20)
]
```

Use `&` for and, `|` for or, and `~` for not. Put each comparison inside parentheses when combining conditions.

### Missing values

```python
df.isna().sum()
df = df.dropna()

df["temperature"] = df["temperature"].fillna(
    df["temperature"].mean()
)
```

> **Scientific check:** Never remove or replace missing observations without explaining and justifying the decision.

### Group and summarise

```python
df.groupby("region")["income"].mean()

summary = (
    df.groupby("region")
      .agg(
          mean_income=("income", "mean"),
          population=("population", "sum")
      )
      .reset_index()
)
```

### Save a table

```python
df.to_csv("analysis_results.csv", index=False)
```

---

## 6. Dates and time series

Dates should be stored as dates rather than ordinary text.

### Convert and index dates

```python
df["date"] = pd.to_datetime(df["date"])
df = df.set_index("date")

df.loc["2020"]
df.loc["2020-01":"2020-12"]
```

### Aggregate and smooth

```python
monthly_temperature = df["temperature"].resample("MS").mean()
annual_precipitation = df["precipitation"].resample("YS").sum()
rolling_temperature = df["temperature"].rolling(30).mean()
```

> **Scientific check:** Match the aggregation to the variable. Temperature is often averaged, while precipitation amounts may be summed. Always confirm the original variable definition and units.

---

## 7. Xarray and multidimensional data

Xarray extends labelled data analysis to multidimensional datasets. It is particularly useful for climate, hydrological and other gridded Earth-system data.

### Open and inspect a dataset

```python
ds = xr.open_dataset("climate_data.nc")

ds
ds.data_vars
ds.coords
ds.dims
ds.attrs
```

A **Dataset** contains related variables. A **DataArray** represents one labelled variable. Dimensions define axes such as time, latitude and longitude; coordinates label positions along those axes.

### Select a variable, time and location

```python
temperature = ds["temperature"]

period = temperature.sel(time=slice("2001", "2020"))

maynooth = temperature.sel(
    latitude=53.38,
    longitude=-6.59,
    method="nearest"
)
```

### Select an area

```python
ireland = temperature.sel(
    latitude=slice(55.5, 51.0),
    longitude=slice(-11.0, -5.0)
)
```

Latitude may run north-to-south or south-to-north. Inspect the coordinate before defining a slice.

### Calculate and resample

```python
temperature.mean()
temperature.mean(dim="time")
temperature.max(dim="time")

monthly = temperature.resample(time="MS").mean()
anomaly = temperature - temperature.mean(dim="time")
```

### Inspect before trusting a calculation

```python
temperature.dims
temperature.shape
temperature.coords
temperature.attrs
```

### Common climate unit conversions

```python
temperature_c = temperature_k - 273.15
precipitation_mm = precipitation_m * 1000
```

> **Scientific check:** Determine whether precipitation represents a rate, an interval total or an accumulated total before converting or aggregating it.

---

## 8. Data visualisation

A figure should communicate evidence clearly. The chart choice and accurate representation of the data matter more than decoration.

### Create a time-series figure

```python
fig, ax = plt.subplots(figsize=(9, 5))

ax.plot(
    df.index,
    df["temperature"],
    color="firebrick",
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

### Plot spatial Xarray data

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

### Save a figure

```python
plt.savefig("figure.png", dpi=300, bbox_inches="tight")
```

### Figure checklist

- Does the title communicate the main finding?
- Are the variable, units, location and period clear?
- Do the chart type and colour scale suit the data?
- Are missing data and uncertainty acknowledged?
- Can the figure be understood without reading the code?
- Does the caption identify the data source?

---

## 9. Errors and debugging

Errors are a normal part of programming. Read the traceback from the final line upward and identify the first part of your own code that failed.

| Error | Likely meaning |
|---|---|
| `NameError` | A variable or package has not been defined. Check spelling and whether earlier cells ran. |
| `KeyError` | A requested column or label does not exist. Inspect the available labels. |
| `FileNotFoundError` | Python cannot find the file. Check its name, path and location. |
| `TypeError` | An operation was applied to an unsuitable object type. Inspect it using `type()`. |
| `ValueError` | The type may be acceptable, but the value, format or shape is unsuitable. |
| `SyntaxError` | Check brackets, quotation marks, colons and indentation. |

### Practical debugging sequence

1. Read the final line of the error.
2. Identify the cell and line that failed.
3. Inspect the object using `type()`, `.shape`, `.head()`, `.dims` or `.coords`.
4. Check spelling, brackets, quotation marks and labels.
5. Change one thing and rerun the cell.
6. Ask for a limited hint only after attempting the diagnosis.

---

## 10. Reproducible notebooks and GitHub

A reproducible notebook should allow another person—or your future self—to understand the decisions and recreate the analysis.

### Notebook checklist

- State a clear title and research question.
- Explain the data source, variables and units.
- Keep package imports together near the beginning.
- Use meaningful variable names.
- Separate stages with informative Markdown headings.
- Include data-quality and plausibility checks.
- Explain important analytical decisions.
- Restart the runtime and run every cell from top to bottom.
- Remove unused code and failed experimental cells from the final version.
- Save the final notebook and commit it to the appropriate GitHub repository.

> **Remember:** Reproducibility is not simply code that runs. The data, assumptions, transformations and interpretation must also be clear.

---

## 11. Using generative AI responsibly

Generative AI can support learning and professional analysis, but it can also conceal gaps in understanding. You remain responsible for every line of code and every result in your notebook.

### Appropriate uses

- Explain an error message in plain language.
- Provide a hint without completing the full task.
- Explain what an existing line or method does.
- Compare two possible approaches.
- Suggest checks for validating a result.
- Review code that you have already attempted.

### Uses that do not demonstrate learning

- Pasting an assessment task into an AI tool.
- Accepting a complete generated workflow.
- Repeatedly generating code until something runs.
- Using functions or methods that you cannot explain.
- Assuming that code is scientifically correct because it executes successfully.

### Recommended learning sequence

> Attempt the task → inspect the error or output → reason about the problem → request a limited hint if needed → modify the code yourself → verify the result.

---

## 12. Learning resources and documentation

The weekly course notebooks provide the main structured learning route. The resources below provide deeper explanations, alternative examples and authoritative documentation.

### Core learning resources

#### [Introduction to Python for Geographic Data Analysis](https://pythongis.org/)

**Recommended open textbook.** Use selected chapters to reinforce the course rather than attempting to complete the entire book at once. It combines Python fundamentals with geographic data-analysis examples.

#### [Project Pythia Foundations](https://foundations.projectpythia.org/)

A community learning resource for Python-based computing in the geosciences. It is particularly valuable for the MSc Climate Change and MSc in GIS/Remote Sensing route and includes open tutorials on:

- NumPy and Pandas;
- dates and calendars;
- Matplotlib;
- NetCDF and Xarray;
- Cartopy;
- Git and GitHub.

#### [Python for Data Analysis, 3rd edition — Wes McKinney](https://wesmckinney.com/book/)

The principal detailed reference for Pandas and general data-analysis workflows. It covers:

- **Interacting with the outside world:** reading and writing common data formats;
- **Preparation:** cleaning, combining, reshaping, selecting and transforming data;
- **Transformation:** applying calculations and grouped operations;
- **Modelling and computation:** connecting data with statistical and computational tools;
- **Presentation:** producing graphical and textual summaries.

### NumPy

- [NumPy documentation](https://numpy.org/doc/stable/)
- [NumPy quickstart](https://numpy.org/doc/stable/user/quickstart.html)

### Pandas

- [Pandas user guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/)
- [10 minutes to Pandas](https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html)
- [Pandas data-wrangling cheat sheet (PDF)](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [Pandas for spreadsheet users](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_spreadsheets.html)
- [Pandas for R users](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_r.html)

### Matplotlib

- [Matplotlib documentation](https://matplotlib.org/)
- [Matplotlib cheat sheets and handouts](https://matplotlib.org/cheatsheets/)

### Xarray

- [Xarray documentation](https://docs.xarray.dev/en/stable/)
- [Xarray in 45 minutes](https://tutorial.xarray.dev/overview/xarray-in-45-min.html)

---

## About this guide

This is a living reference. Examples and links may be refined as the courses develop. Corrections and suggestions are welcome.

Maintained by **Shaun Harrigan**, ICARUS Climate Research Centre, Department of Geography, Maynooth University.
