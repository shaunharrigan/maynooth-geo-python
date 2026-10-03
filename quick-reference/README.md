# Python Quick Reference Guide

Practical Python for geographical data analysis using Google Colab, NumPy, Pandas, Xarray and Matplotlib.

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
7. [Xarray and multidimensional data](#7-xarray-and-multidimensional-data)
8. [Data visualisation](#8-data-visualisation)
9. [Errors and debugging](#9-errors-and-debugging)
10. [Reproducible notebooks and GitHub](#10-reproducible-notebooks-and-github)
11. [Using generative AI responsibly](#11-using-generative-ai-responsibly)
12. [Learning resources and documentation](#12-learning-resources-and-documentation)

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
import xarray as xr
import matplotlib.pyplot as plt
```

These shortened names are standard conventions:

| Package | Short name | Used for |
|---|---|---|
| NumPy | `np` | Numerical arrays and calculations |
| Pandas | `pd` | Tabular data |
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

## Conditions and loops

An `if` statement runs code when a condition is true:

```python
if temperature > 20:
    print("Warm")
else:
    print("Not warm")
```

A `for` loop repeats an operation:

```python
for station in stations:
    print(station)
```

> **Important:** Indentation is part of Python syntax.

## Functions, methods and attributes

You will encounter several slightly different ways of asking Python to do something:

```python
print(temperature)          # function

temperature.mean()          # method

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
temperature.mean()
```

means: calculate the mean of the object called `temperature`.

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

# 7. Xarray and multidimensional data

Xarray is particularly useful for climate, hydrological and other gridded Earth-system data.

## Open a dataset

```python
import xarray as xr

ds = xr.open_dataset("climate_data.nc")
```

## Inspect a dataset

```python
ds
```

displays an overview of the complete dataset.

Useful attributes include:

```python
ds.data_vars   # data variables

ds.coords      # coordinates

ds.dims        # dimensions

ds.attrs       # metadata
```

A **Dataset** can contain several related variables.

A **DataArray** represents one labelled variable.

Dimensions might include:

- time;
- latitude;
- longitude.

## Select a variable

```python
temperature = ds["temperature"]
```

## Select a time period

```python
period = temperature.sel(
    time=slice("2001", "2020")
)
```

## Select a location

```python
maynooth = temperature.sel(
    latitude=53.38,
    longitude=-6.59,
    method="nearest"
)
```

## Select an area

```python
ireland = temperature.sel(
    latitude=slice(55.5, 51.0),
    longitude=slice(-11.0, -5.0)
)
```

Latitude can run north-to-south or south-to-north. Always inspect the coordinate before defining a slice.

## Calculate across dimensions

```python
temperature.mean()
```

calculates a mean across every dimension.

To calculate the mean through time:

```python
temperature.mean(dim="time")
```

Maximum through time:

```python
temperature.max(dim="time")
```

## Resample and calculate anomalies

```python
monthly = temperature.resample(time="MS").mean()
```

```python
anomaly = temperature - temperature.mean(dim="time")
```

## Inspect before calculating

Useful checks include:

```python
temperature.dims

temperature.shape

temperature.coords

temperature.attrs
```

These help you understand what the data represent before performing calculations.

## Common climate unit conversions

Kelvin to degrees Celsius:

```python
temperature_c = temperature_k - 273.15
```

Metres to millimetres:

```python
precipitation_mm = precipitation_m * 1000
```

> **Scientific check:** Always check the variable metadata and units before converting or aggregating data.

---

# 8. Data visualisation

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

# 9. Errors and debugging

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

# 10. Reproducible notebooks and GitHub

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

# 11. Using generative AI responsibly

Generative AI can support learning and professional data analysis, but it can also hide gaps in understanding.

You remain responsible for every line of code and every result in your notebook.

> **Important:** Module-specific assessment rules always take precedence over this general guidance.

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

# 12. Learning resources and documentation

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

### Xarray

- Xarray documentation: https://docs.xarray.dev/en/stable/
- Xarray in 45 minutes: https://tutorial.xarray.dev/overview/xarray-in-45-min.html

---

# About this guide

This is a **living reference** and will develop alongside the course.

The weekly notebooks are the main route through the module. Use this guide when you need to **remember syntax, revisit something introduced in class, or find out where to look next**.

Corrections and suggestions are welcome.

Maintained by **Shaun Harrigan**, ICARUS Climate Research Centre, Department of Geography, Maynooth University.
