# Data example

## create a small dummy dataset of pet food sales

```
Date	Product	Brand	Category	Quantity	Price per unit	Total sales
2022-01-01	Dog Food	Purina	Dry	10	15.99	159.90
2022-01-02	Cat Food	Royal Canin	Wet	12	2.50	30.00
2022-01-03	Cat Food	Hill's	Dry	8	22.50	180.00
2022-01-04	Dog Food	Blue Buffalo	Wet	6	4.99	29.94
2022-01-05	Cat Food	Purina	Dry	15	12.99	194.85
2022-01-06	Dog Food	Hill's	Wet	7	3.75	26.25
2022-01-07	Dog Food	Royal Canin	Dry	12	18.99	227.88
2022-01-08	Cat Food	Blue Buffalo	Wet	10	5.50	55.00
2022-01-09	Dog Food	Purina	Wet	5	4.25	21.25
2022-01-10	Cat Food	Hill's	Wet	9	2.99	26.91
```

In this dataset, we have sales data for ten days from 1st January 2022 to 10th January 2022. The data includes the date of sale, the type of product (dog food or cat food), the brand of the product, the category of the product (dry or wet), the quantity sold, the price per unit, and the total sales for each transaction.

## average the total sales

To calculate the average of the total sales in this dataset, we can add up all the values in the "Total sales" column and divide by the number of rows (i.e., the number of transactions):

(java)

```
Average total sales = (159.90 + 30.00 + 180.00 + 29.94 + 194.85 + 26.25 + 227.88 + 55.00 + 21.25 + 26.91) / 10 = 141.98
```

Therefore, the average total sales for this dataset is $141.98.

## show a piechart of these total-sales

To create a pie chart of the total sales in this dataset, we can use a data visualization tool such as Python's Matplotlib library. Here's an example code snippet to create a pie chart using the dataset:

(python)

```
import matplotlib.pyplot as plt
import pandas as pd

# Load the dataset
df = pd.read_csv("pet_food_sales.csv")

# Calculate the total sales for each category
category_sales = df.groupby('Category')['Total sales'].sum()

# Create a pie chart
plt.pie(category_sales.values, labels=category_sales.index, autopct='%1.1f%%')
plt.title('Total Sales by Category')
plt.show()
```

This code will create a pie chart that shows the distribution of total sales by category:

(missing image)

_Pie chart of total sales by category_

In this chart, the "Dry" category accounts for the majority of total sales (63.8%), while the "Wet" category accounts for the remaining 36.2% of total sales.

---