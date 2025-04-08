# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
df['Order Date'] = pd.to_datetime(df['Order Date'], dayfirst=True) 
resampled_data = df.resample('Y', on='Order Date')['Sales'].sum().to_frame()
resampled_data.index = resampled_data.index.year  # Extract year
resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'Order Date': 'Year'}, inplace=True)
years = resampled_data['Year'].tolist()
sales = resampled_data['Sales'].tolist()
X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, sales)]
n = len(years)
b = (n * sum(xy) - sum(sales) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(sales) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]
print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
```
B- POLYNOMIAL TREND ESTIMATION
```
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, sales)]
coeff = [[n, sum(X), sum(x2)],
         [sum(X), sum(x2), sum(x3)],
         [sum(x2), sum(x3), sum(x4)]]
Y = [sum(sales), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)
solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]
```
### OUTPUT
# A - LINEAR TREND ESTIMATION

![image](https://github.com/user-attachments/assets/4049a84b-7b2f-457b-a574-629d1ffdf390)

# B- POLYNOMIAL TREND ESTIMATION

![image](https://github.com/user-attachments/assets/3522a289-dba5-42f6-9553-a369b96c1be6)

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
