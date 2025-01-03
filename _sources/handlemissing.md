# Missing Data Handling

## **Overview**
The `data_processing.py` module provides a function for handling missing data in single-case experimental design datasets. This module ensures the integrity and continuity of the data by offering functionality to interpolate missing values, which is essential for robust analysis.



### **Function: `fill_missing`**

#### **Purpose**
The `fill_missing` function fills in missing values in a single-case dataset using linear interpolation. It ensures the dataset is complete and sorted by the measurement time variable before processing.



#### **Parameters**
- **`data`**: A Pandas DataFrame containing the single-case dataset.  
- **`dvar`**: The name of the dependent variable column in the DataFrame, representing the primary measurement of interest.  
- **`mvar`**: The name of the measurement time column in the DataFrame, ensuring the data is processed in temporal order.  
- **`na_rm`** (default: `True`): A boolean flag indicating whether missing values in the dependent variable column should be interpolated. When `True`, linear interpolation is applied to fill the gaps.



#### **Returns**
- A Pandas DataFrame with missing values in the dependent variable column filled using linear interpolation (if `na_rm=True`).


## **Usage Example**

### **Input Dataset**
```python
import pandas as pd

data = pd.DataFrame({
    "values": [10, None, 15, None, 20],
    "time": [1, 2, 3, 4, 5]
})
```

#### **Filling Missing Values**
```python
from data_processing import fill_missing

# Fill missing values in the dataset
processed_data = fill_missing(data, dvar="values", mvar="time", na_rm=True)
print(processed_data)
```

#### **Output**
```
   values  time
0    10.0     1
1    12.5     2
2    15.0     3
3    17.5     4
4    20.0     5
```



## **Key Notes**
1. **Sorting by Measurement Time**: The function automatically sorts the data by the `mvar` column to ensure proper interpolation.
2. **Interpolation Method**: Currently, the function uses linear interpolation. For other methods, users can modify the interpolation line in the code as needed.
3. **When `na_rm=False`**: If `na_rm` is set to `False`, the function does not fill the missing values, leaving them as `NaN`.



## **Error Handling**
- Ensure that the `data` parameter is a valid Pandas DataFrame.
- The `dvar` and `mvar` parameters must be column names present in the DataFrame; otherwise, a KeyError will be raised.
- Missing values in the dependent variable column are handled only when `na_rm=True`.
