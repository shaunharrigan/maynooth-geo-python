# Python Quick Reference Guide

Practical Python for geographical data analysis using Google Colab, NumPy, Pandas, Xarray and Matplotlib.

This guide supports **GY674: Earth Science Data Analysis in Python** and **GY675: Visualising Inequality** at Maynooth University. It is also intended as a useful starting point for postgraduate researchers and staff who are new to Python.

> **How to use this guide:** This is a complete reference, available from the beginning of the course. You are not expected to understand every section immediately. Use it to recall methods already introduced, find reliable documentation and identify what you need to learn next. The weekly notebooks provide the structured route through the course.

The short examples illustrate common patterns. Most are not intended to form one continuous analysis: run the relevant package imports first and replace example filenames and variable names with those used in your own dataset.

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

Try this in a code cell:

```python
print("Hello from Python")  # Display a short message
```

The text after `#` is a **comment**. Python ignores comments when running the code; they are notes for the person reading it.

### Writing in a text cell

Text cells use **Markdown**, a simple way to format explanatory text:

```markdown
# Main heading
## Smaller heading

**bold text** and *italic text*

- first item
- second item

[link text](https://example.com)
```

Use text cells to explain the purpose of an analysis, describe the data and interpret results. A notebook should not consist of unexplained code alone.

### The runtime

The **runtime** is the temporary remote computer session that executes the Python code. Variables, files uploaded only to the session and packages installed during the session are lost when it restarts or disconnects. A notebook saved in Google Drive remains available, but you may need to rerun its cells when you reconnect.

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

### Accessing files in Colab

Small files can be uploaded using the **Files** panel on the left of Colab. These uploads are temporary and disappear when the runtime is reset.

To access files stored in your Google Drive:

```python
from google.colab import drive

drive.mount("/content/drive")  # Authorise Colab to access your Drive
```

A file in Drive can then be opened using its full path, for example:

```python
file_path = "/content/drive/MyDrive/GY674/data.csv"  # Store the file location
df = pd.read_csv(file_path)  # Read the CSV file into a Pandas DataFrame
```

Only mount Drive in notebooks you trust, because code in the notebook can access files available through the mounted Drive.

---

## 2. Import conventions

The Python community uses standard abbreviations for widely used packages:

```python
import numpy as np               # Numerical arrays and calculations
import pandas as pd              # Tabular data analysis
import xarray as xr              # Labelled multidimensional data
import matplotlib.pyplot as plt  # Data visualisation
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

type(temperature)   # Show the type of object stored in the variable
print(temperature)  # Display the value stored in the variable
```

Python is case-sensitive: `temperature` and `Temperature` are different names.

A variable name should describe the information it stores. Use lower-case words separated by underscores, such as `annual_temperature`. A variable name cannot contain spaces or begin with a number.

### Collections

```python
stations = ["Maynooth", "Dublin", "Derry"]          # list
coordinates = (53.38, -6.59)                          # tuple
station_info = {"name": "Maynooth", "elevation": 48}  # dictionary
```

- A **list** is an ordered collection that can be changed after it is created.
- A **tuple** is an ordered collection usually used for values that belong together, such as coordinates.
- A **dictionary** stores values using named keys; for example, `station_info["name"]` returns `"Maynooth"`.

Python starts counting at zero:

```python
stations[0]       # first item
stations[-1]      # final item
stations[0:2]     # first two items; final position is excluded
```

### Operators and comparisons

```python
temperature_k = 291.55  # Assign a temperature in kelvin
temperature_c = temperature_k - 273.15  # Convert kelvin to degrees Celsius
is_warm = temperature_c > 20  # True if temperature_c is above 20
is_valid = (temperature_c > -50) and (temperature_c < 60)  # Plausibility check
```

- `=` assigns a value.
- `==` tests whether values are equal.
- `!=` means not equal.
- `>`, `<`, `>=` and `<=` compare values.
- `and`, `or` and `not` combine ordinary Python conditions. Pandas filters use `&`, `|` and `~` instead, as shown later.

### Conditions and loops

```python
if temperature > 20:
    print("Warm")      # Run this line when the condition is True
else:
    print("Not warm")  # Run this line when the condition is False
```

```python
for station in stations:
    print(station)  # Repeat once for each item in the list
```

Indentation is part of Python syntax.

### Functions, methods and attributes

```python
print(temperature)          # function
df.head()                   # method
df.shape                    # attribute
pd.read_csv("data.csv")     # function from Pandas
```

Parentheses call a function or method. Attributes such as `.shape` describe an object and do not use parentheses.

### Define a simple function

A function packages a reusable operation. Inputs are placed inside the parentheses, and `return` sends the result back:

```python
def kelvin_to_celsius(temperature_k):
    """Convert temperature from kelvin to degrees Celsius."""
    temperature_c = temperature_k - 273.15
    return temperature_c


kelvin_to_celsius(291.55)  # Returns 18.4
```

---

## 4. NumPy arrays

NumPy (**Numerical Python**) provides arrays and numerical operations. An array stores data in one or more dimensions. A one-dimensional array resembles a list; a two-dimensional array resembles a table or grid.

### Create and inspect an array

```python
values = np.array([12.1, 14.5, 13.8])

values.shape  # Length of each dimension
values.dtype  # Data type stored in the array
values.ndim   # Number of dimensions
values.size   # Total number of values
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
values.mean()       # Arithmetic mean
values.min()        # Smallest value
values.max()        # Largest value
values.sum()        # Sum of all values
np.median(values)   # Median: middle value when ordered
np.std(values)      # Standard deviation: spread around the mean
```

> **Common mistake:** Python lists and NumPy arrays can look similar but behave differently during calculations. Use `type()` when uncertain.

---

## 5. Pandas and tabular data

Pandas is used for labelled tabular data. A **DataFrame** contains rows and columns; a single column is usually a **Series**.

### Read and inspect a CSV file

```python
df = pd.read_csv("data.csv")  # Read a comma-separated file into a DataFrame

df.head()      # Display the first 5 rows
df.tail()      # Display the final 5 rows
df.info()      # Summarise columns, data types and non-missing values
df.describe()  # Calculate summary statistics for numerical columns
df.shape       # Return (number of rows, number of columns)
df.columns     # List the column names
df.dtypes      # Show the data type of each column
```

`"data.csv"` is an example file path. Replace it with the name or path of your own file. In Colab, a file uploaded only through the Files panel is temporary and must be uploaded again after the runtime restarts.

### Select columns and rows

```python
df["temperature"]             # Select one column as a Series
df[["date", "temperature"]]   # Select two columns as a DataFrame

df.loc[0:4, ["date", "temperature"]]  # Labels 0 to 4; end label included
df.iloc[0:5, 0:2]                      # First 5 rows and first 2 columns
```

Selecting one column normally returns a Series. Selecting a list of columns returns a DataFrame. `.loc` selects by labels; `.iloc` selects by numerical position and excludes the final position in a slice.

### Filter observations

```python
warm = df[df["temperature"] > 20]  # Keep rows above 20°C

wet_and_warm = df[
    (df["precipitation"] > 0) &   # Precipitation is above zero AND
    (df["temperature"] > 20)      # temperature is above 20°C
]
```

Use `&` for and, `|` for or, and `~` for not. Put each comparison inside parentheses when combining conditions.

### Missing values

```python
df.isna().sum()  # Count missing values in each column

# Option 1: create a copy containing only complete rows
df_complete = df.dropna()

# Option 2: replace missing temperatures with the column mean
df["temperature"] = df["temperature"].fillna(
    df["temperature"].mean()
)
```

These are alternative examples, not an instruction to apply both. The appropriate treatment depends on what the missing values represent.

> **Scientific check:** Never remove or replace missing observations without explaining and justifying the decision.

### Group and summarise

```python
df.groupby("region")["income"].mean()  # Mean income for each region

summary = (
    df.groupby("region")  # Form one group for each region
      .agg(
          mean_income=("income", "mean"),      # Mean income in each group
          population=("population", "sum")     # Total population in each group
      )
      .reset_index()  # Return region from the index to an ordinary column
)
```

### Save a table

```python
df.to_csv("analysis_results.csv", index=False)  # Save without an extra index column
```

---

## 6. Dates and time series

Dates should be stored as dates rather than ordinary text.

### Convert and index dates

```python
df["date"] = pd.to_datetime(df["date"])  # Convert text into datetime values
df = df.set_index("date")  # Use dates as the row labels

df.loc["2020"]                  # All observations in 2020
df.loc["2020-01":"2020-12"]    # January to December 2020
```

### Aggregate and smooth

```python
monthly_temperature = df["temperature"].resample("MS").mean()  # Monthly means
annual_precipitation = df["precipitation"].resample("YS").sum()  # Annual totals
rolling_temperature = df["temperature"].rolling(30).mean()  # 30-row moving mean
```

> **Scientific check:** Match the aggregation to the variable. Temperature is often averaged, while precipitation amounts may be summed. Always confirm the original variable definition and units.

---

## 7. Xarray and multidimensional data

Xarray extends labelled data analysis to multidimensional datasets. It is particularly useful for climate, hydrological and other gridded Earth-system data.

### Open and inspect a dataset

```python
ds = xr.open_dataset("climate_data.nc")  # Open a NetCDF file as an Xarray Dataset

ds           # Display an interactive overview of the complete Dataset
ds.data_vars  # Data variables
ds.coords     # Coordinate labels
ds.dims       # Dimension names and lengths
ds.attrs      # Dataset metadata
```

A **Dataset** contains related variables. A **DataArray** represents one labelled variable. Dimensions define axes such as time, latitude and longitude; coordinates label positions along those axes.

Names vary between datasets: for example, coordinates may be called `latitude` and `longitude`, or `lat` and `lon`. Always inspect the dataset before copying a selection example.

### Select a variable, time and location

```python
temperature = ds["temperature"]  # Select one variable as a DataArray

period = temperature.sel(time=slice("2001", "2020"))  # Select a time period

maynooth = temperature.sel(
    latitude=53.38,     # Target latitude
    longitude=-6.59,   # Target longitude
    method="nearest"   # Use the nearest available grid cell
)
```

### Select an area

```python
ireland = temperature.sel(
    latitude=slice(55.5, 51.0),    # Northern to southern boundary
    longitude=slice(-11.0, -5.0)   # Western to eastern boundary
)
```

Latitude may run north-to-south or south-to-north. Inspect the coordinate before defining a slice.

### Calculate and resample

```python
temperature.mean()                 # Mean across every dimension
temperature.mean(dim="time")      # Mean through time at each location
temperature.max(dim="time")       # Maximum through time at each location

monthly = temperature.resample(time="MS").mean()  # Monthly mean values
anomaly = temperature - temperature.mean(dim="time")  # Difference from time mean
```

### Inspect before trusting a calculation

```python
temperature.dims    # Dimension names, for example (time, latitude, longitude)
temperature.shape   # Number of values along each dimension
temperature.coords  # Coordinate labels and values
temperature.attrs   # Metadata such as units and a descriptive name
```

### Common climate unit conversions

```python
# Select variables whose original units are kelvin and metres
temperature_k = ds["temperature"]
precipitation_m = ds["precipitation"]

temperature_c = temperature_k - 273.15  # Convert kelvin to degrees Celsius
precipitation_mm = precipitation_m * 1000  # Convert metres to millimetres
```

Here, names ending in `_k`, `_c`, `_m` and `_mm` make the assumed units explicit. Check the variable's metadata before converting it.

> **Scientific check:** Determine whether precipitation represents a rate, an interval total or an accumulated total before converting or aggregating it.

---

## 8. Data visualisation

A figure should communicate evidence clearly. The chart choice and accurate representation of the data matter more than decoration.

### Create a time-series figure

```python
fig, ax = plt.subplots(figsize=(9, 5))  # Create a figure and one plotting area

ax.plot(
    df.index,            # Values for the horizontal axis
    df["temperature"],  # Values for the vertical axis
    color="firebrick",  # Line colour
    linewidth=1.5        # Line thickness
)

ax.set(
    title="Annual temperature at Maynooth",  # Figure title
    xlabel="Year",                            # Horizontal-axis label
    ylabel="Temperature (°C)"                 # Vertical-axis label and units
)

ax.grid(alpha=0.25)  # Add a light grid
plt.tight_layout()   # Adjust spacing so labels are not cut off
plt.show()           # Display the completed figure
```

### Plot spatial Xarray data

```python
fig, ax = plt.subplots(figsize=(8, 6))  # Create a figure and plotting area

temperature.mean(dim="time").plot(
    ax=ax,                                      # Draw on this plotting area
    cmap="RdBu_r",                             # Select a colour map
    cbar_kwargs={"label": "Temperature (°C)"}  # Label the colour bar
)

ax.set_title("Mean annual temperature, 2001–2020")  # Add a title
plt.show()  # Display the completed map
```

### Save a figure

```python
fig.savefig(
    "figure.png",       # Output filename
    dpi=300,             # Image resolution in dots per inch
    bbox_inches="tight"  # Remove unnecessary surrounding whitespace
)
```

Save the figure after creating it and before closing or clearing it. `dpi=300` produces a high-resolution raster image, while `bbox_inches="tight"` reduces unnecessary surrounding whitespace.

### Figure checklist

- Does the title communicate the main finding?
- Are the variable, units, location and period clear?
- Do the chart type and colour scale suit the data?
- Are missing data and uncertainty acknowledged?
- Can the figure be understood without reading the code?
- Does the caption identify the data source?
- Are colours and labels accessible and readable when printed or viewed by someone with colour-vision deficiency?

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

A **repository** is a project folder tracked by GitHub. A **commit** is a saved checkpoint with a short message explaining what changed. GitHub stores the notebook and its history; Colab provides the environment in which the notebook runs.

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
- Do not commit passwords, API keys, personal data or restricted datasets.

> **Remember:** Reproducibility is not simply code that runs. The data, assumptions, transformations and interpretation must also be clear.

---

## 11. Using generative AI responsibly

Generative AI can support learning and professional analysis, but it can also conceal gaps in understanding. You remain responsible for every line of code and every result in your notebook.

Any module-specific assessment rules take precedence over this general guidance.

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

The weekly course notebooks provide the main structured route through the course. The resources below offer additional explanations, worked examples and authoritative documentation.

### Recommended course textbook

#### [Introduction to Python for Geographic Data Analysis](https://pythongis.org/)

**Tenkanen, Heikinheimo and Whipp (2025)**

This is the recommended free online textbook supporting the weekly laboratory notebooks. Selected sections will be signposted during the course. You are **not expected to read or complete the entire book**.

> **Reference:** Tenkanen, H., Heikinheimo, V. and Whipp, D. (2025) *Introduction to Python for Geographic Data Analysis* [e-book]. Available at: [https://pythongis.org/](https://pythongis.org/) (Accessed: 12 September 2026).

### Additional learning resources

#### [Project Pythia Foundations](https://foundations.projectpythia.org/)

Project Pythia is a community learning resource for Python-based computing in the geosciences. It provides open tutorials covering:

- NumPy and Pandas;
- dates and calendars;
- Matplotlib;
- NetCDF and Xarray;
- Cartopy;
- Git and GitHub.

> **Best suited to:** MSc Climate Change, Earth Science, GIS and Remote Sensing students who want to extend the material introduced in class.

#### [Python for Data Analysis, 3rd edition — Wes McKinney](https://wesmckinney.com/book/)

A detailed open-access resource for Pandas and general data-analysis workflows. It covers:

- **Interacting with the outside world:** reading and writing common data formats;
- **Preparation:** cleaning, combining, reshaping, selecting and transforming data;
- **Transformation:** applying calculations, aggregations and grouped operations;
- **Modelling and computation:** connecting data with statistical and computational tools;
- **Presentation:** producing graphical and textual summaries.

> **Best suited to:** students and researchers who expect to use Pandas extensively. This is a reference and extension resource rather than required course reading.

### Package documentation and quick guides

Official documentation provides the most complete and current information about each package. You are not expected to read it from beginning to end. Use it to look up particular functions, methods and examples.

#### Python and Google Colab

- [Official Python tutorial](https://docs.python.org/3/tutorial/)
- [Google Colab frequently asked questions](https://research.google.com/colaboratory/faq.html)

#### NumPy

- [NumPy documentation](https://numpy.org/doc/stable/)
- [NumPy quickstart](https://numpy.org/doc/stable/user/quickstart.html)

#### Pandas

- [Pandas user guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/)
- [10 minutes to Pandas](https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html)
- [Pandas data-wrangling cheat sheet (PDF)](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [Pandas for spreadsheet users](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_spreadsheets.html)
- [Pandas for R users](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_r.html)

#### Matplotlib

- [Matplotlib documentation](https://matplotlib.org/stable/)
- [Matplotlib cheat sheets and handouts](https://matplotlib.org/cheatsheets/)

#### Xarray

- [Xarray documentation](https://docs.xarray.dev/en/stable/)
- [Xarray in 45 minutes](https://tutorial.xarray.dev/overview/xarray-in-45-min.html)

---

## About this guide

This is a living reference. Examples and links may be refined as the courses develop. Corrections and suggestions are welcome.

Maintained by **Shaun Harrigan**, ICARUS Climate Research Centre, Department of Geography, Maynooth University.
