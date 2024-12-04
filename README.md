# Python & Power BI Vietnam Housing Price Project
This project leverages **Python** (pandas, seaborn, matplotlib, scikit-learn) for comprehensive data cleaning and transformation, ensuring the dataset is optimized for regression analysis. Multiple regression techniques, including **Multiple Linear Regression**, **Polynomial Regression**, and **Ridge Regression**, are employed to determine the most effective model for predicting housing prices in Vietnam. Additionally, the project utilizes the advanced visualization capabilities of **Power BI** to create interactive graphs and charts, providing actionable insights into Vietnam's housing market.

## 1. Dataset Overview
The dataset comprises over **30,000 house listings** in Vietnam for the year 2024. However, a significant number of null values are present across various columns in the original dataset, rendering it unsuitable for immediate data analysis. As a result, proper data cleaning and transformation processes are required to prepare the data for analysis. The dataset is available on Kaggle and can be downloaded [here](https://www.kaggle.com/datasets/nguyentiennhan/vietnam-housing-dataset-2024).

![image](https://github.com/user-attachments/assets/bf175278-6cf4-4fa6-b22e-e4472f469d87)

### Columns
- Address: The complete address of the property, including details such as the project name, street, ward, district, and city. **(object)**
- Area: The total area of the property, measured in square meters. **(float64)**
- Frontage: The width of the front side of the property, measured in meters. **(float64)**
- Access Road: The width of the road providing access to the property, measured in meters. **(float64)**
- House Direction: The cardinal direction the front of the house is facing (e.g., East, West, North, South). **(float64)**
- Balcony Direction: The cardinal direction the balcony is facing. **(object)**
- Floors: The total number of floors in the property. **(object)**
- Bedrooms: The number of bedrooms in the property. **(float64)**
- Bathrooms: The number of bathrooms in the property. **(float64)**
- Legal Status: Indicates the legal status of the property, such as whether it has a certificate of ownership or is under a sale contract. **(float64)**
- Furniture State: Indicates the state of furnishing in the property, such as fully furnished, partially furnished, or unfurnished. **(object)**
- Price: The price of the property, represented in billions of Vietnamese Dong (VND). **(object)**

## 2. Correlation
A **critical** step prior to implementing regression models is assessing the correlation between the dependent variable and the independent variables. This involves identifying which variables exhibit strong correlations and significantly influence the fluctuations of the target variable, in this case **Price**, and determining which variables are irrelevant and may not contribute meaningfully to the models. 

- The **heatmap** below offers a clearer visualization of this relationship between **numerical** variables: higher correlation values between variables indicate a stronger association.

![image](https://github.com/user-attachments/assets/65fc9399-8c86-4465-af76-fee546fb4b04)

- For **categorical** variables, one great way to visualize the correlation between variables is using **boxplots**:

![image](https://github.com/user-attachments/assets/8c60d564-0f2f-44fc-b369-b6b7dbb5da10)
![image](https://github.com/user-attachments/assets/398135a0-02e3-45c4-ad6e-97876075a629)

- As you can see, no clear relationship is present between Legal status/Furniture state and Price. Also, considering the high number of null values in these 2 columns, they are deemed not fit for regression models.

## 3. Data Cleaning & Transformation
- Following a series of data preprocessing steps, including identifying outliers and duplicated values, dropping null values, renaming and removing irrelevant columns, and transforming the address column, the dataset has been refined to 12,296 records across 7 columns:

![image](https://github.com/user-attachments/assets/ed520483-7905-4f1e-9c0f-57056a9da4f0)
![image](https://github.com/user-attachments/assets/f4660a0b-3785-4799-bb7b-91aeb8959147)

- The decision to reduce the **address** column to **three unique values** (HN, HCM, and Others) stems from the fact that **Hanoi and Ho Chi Minh City** are the two **most densely populated cities** in Vietnam. Their population density far surpasses that of other cities in the country. The combination of limited land availability, resulting in a **constrained housing supply**, and a large population driving **high housing demand**, consistently leads to **significantly higher housing prices** in Hanoi and Ho Chi Minh City compared to other regions.


