# SingleCaseData Class

## **Overview**
The `SingleCaseData` class provides a streamlined way to organize and manage single-case experimental design data. This class enables users to define experimental phases, structure their data into a consistent format, and export it for further analysis or presentation. It is designed to accommodate various input formats and offers flexibility in defining phase designs and metadata.

---

### **Usage Guide**

#### **Creating a SingleCaseData Object**
The `SingleCaseData` class can be initialized using raw values, phases, and optional parameters. Alternatively, users can provide a pre-structured DataFrame containing the data.

##### **Basic Initialization**
```python
from scapyp import SingleCaseData

# Example with raw values
case_data = SingleCaseData(
    values=[10, 20, 15, 25],
    phase=["A", "A", "B", "B"],
    name="Case1"
)
```

##### **Initialization with a DataFrame**
```python
import pandas as pd

df = pd.DataFrame({
    "values": [10, 20, 15, 25],
    "phase": ["A", "A", "B", "B"],
    "case": ["Case1"] * 4
})

case_data = SingleCaseData(data=df, dvar="values", pvar="phase")
```


#### **Exploring the Data**
Once initialized, the `SingleCaseData` object creates a structured DataFrame that can be accessed via the `.df` attribute:

```python
print(case_data.df)
```


#### **Defining Phases**
The `SingleCaseData` class supports multiple ways to define experimental phases, including:

- **Manual Specification**: Directly input phase labels.
- **Phase Starts**: Define start points for each phase.
- **Phase Design**: Specify the number of observations per phase.
- **B_start**: Indicate where phase "B" begins.

##### **Using Phase Starts**
```python
case_data = SingleCaseData(
    values=[10, 20, 15, 25, 30],
    phase_starts={"A": 1, "B": 3}
)
```

##### **Using Phase Design**
```python
case_data = SingleCaseData(
    values=[10, 20, 15, 25],
    phase_design={"A": 2, "B": 2}
)
```

##### **Using B_start**
```python
case_data = SingleCaseData(
    values=[10, 20, 15, 25],
    B_start=3
)
```


#### **Exporting Data**
The `SingleCaseData` class supports exporting data to various formats, including HTML, CSV, and Excel. Users can customize the export with captions, footnotes, and column selections.

##### **Export as HTML**
```python
html_output = case_data.export(format="html", caption="Case Data Summary")
print(html_output)
```

##### **Export as CSV**
```python
case_data.export(filename="case_data.csv", format="csv")
```

##### **Export as Excel**
```python
case_data.export(filename="case_data.xlsx", format="xlsx")
```


#### **Combining Multiple Cases**
The `SingleCaseData.as_long_dataframe` method merges multiple `SingleCaseData` objects into a single long-form DataFrame, enabling comparative analyses across cases.

##### **Example**
```python
case1 = SingleCaseData(values=[10, 20], phase=["A", "B"], name="Case1")
case2 = SingleCaseData(values=[15, 25], phase=["A", "B"], name="Case2")

long_df = SingleCaseData.as_long_dataframe([case1, case2])
print(long_df)
```


#### **Key Methods**

- **Initialization Parameters**:
  - `values`: List of numerical data points.
  - `phase`: List of phase labels corresponding to data points.
  - `name`: Name of the case (optional).
  - `B_start`: Integer indicating the start of phase "B" (optional).
  - `phase_design`: Dictionary specifying the length of each phase (optional).
  - `phase_starts`: Dictionary defining start points for each phase (optional).

- **Export Method Parameters**:
  - `filename`: Path to save the exported file.
  - `format`: Output format (`html`, `csv`, or `xlsx`).
  - `caption`: Caption for HTML exports.
  - `footnote`: Footnote for HTML exports.
  - `round_decimals`: Number of decimal places to round numeric data.
  - `columns`: Specific columns to include in the export.


### **Examples**

#### **Basic Workflow**
```python
# Define single-case data
case_data = SingleCaseData(
    values=[10, 20, 15, 25],
    phase=["A", "A", "B", "B"],
    name="Example Case"
)

# Export to CSV
case_data.export(filename="example_case.csv", format="csv")

# Combine with another case
case2 = SingleCaseData(values=[5, 10], phase=["A", "B"], name="Case2")
combined = SingleCaseData.as_long_dataframe([case_data, case2])
print(combined)
```

### **Error Handling**

- Ensure the `values` list matches the length of `phase` if specified manually.
- Specify a valid file path when saving exported data.
- Use supported formats (`html`, `csv`, or `xlsx`) for exports.

