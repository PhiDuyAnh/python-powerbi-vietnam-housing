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
- Furthermore, this approach also aligns with my decision to use **dummy variables** (0 and 1 value variables) in my regression models later on.

## 4. Regression Models

### Setting up Dummy Variables

As previously discussed, due to the **impact** of geographical regions on house prices (particularly Hanoi and Ho Chi Minh City), I decided to create **2 dummy variables** (HN an HCMC) for the regression models.
- HN = 1 and HCMC = 0 represent houses located in Hanoi.
- HN = 0 and HCMC = 1 represent houses located in Ho Chi Minh City.
- HN = 0 and HCMC = 0 represent houses located in cities other than Hanoi and Ho Chi Minh City.

![image](https://github.com/user-attachments/assets/c1de635a-915d-4ca8-ae09-12c97d78b4cc)
![image](https://github.com/user-attachments/assets/c02cdabc-02ce-4adb-8226-7486589e1250)

### Results
- **R² score** and **MSE (Mean Squared Error)** are the 2 metrics used to evaluate the models. Generally, a higher R² score and a lower MSE indicate a better-performing model. However, please bear in mind that there are also lots of **factors** to be taken into account such as the data itself may require different types of model, the true relationship between the variables, unobserved factors, etc.
- Given the **simplicity** of the **Multiple Linear Regression** model for this dataset, which resulted in a **lower** R² score, I opted to implement a **Polynomial Regression** model and determined the **3rd order** as the most optimal choice.
- **Ridge Regression** was employed to **reduce** the **magnitude of the coefficients** when working with **Polynomial Features**, leveraging the **hyperparameter Alpha**. Through the use of **GridSearchCV**, an optimal **Alpha** value of **10** was identified as the best estimator for the model.
- Based **solely** on the results of **R² score** and **MSE** value, **Ridge Regression** is selected as the best model for this dataset. However, there remains a lot of **rooms for improvement**!

![image](https://github.com/user-attachments/assets/9a1d2899-6f57-48b3-a60c-a10cccb2645b)

## 5. Data Visualization using Power BI
**Power BI** stands out as one of the most **effective** tools for **visualizing** and **extracting key insights** from **raw data**. By utilizing its capabilities to create an **interactive dashboard**, we can gain a **deeper understanding** of the Vietnam Housing dataset, **uncover patterns**, and **derive valuable insights** into the Vietnamese real estate market.

![image](https://github.com/user-attachments/assets/0d9fac14-a45d-4fd3-bb69-1ed2810de32e)
![image](https://github.com/user-attachments/assets/56c8002d-8003-4970-b5cf-6239fade733a)

### *Key Metrics*
Leveraging **DAX (Data Analysis Expressions)** to calculate these measures:
- Total House Listings
- Average House Price (in billion VND)
- Average House Area (in square meters)
- Median Price per Square Meter

### *Summary of Insights*
1. **Ho Chi Minh City** accounts for the **largest proportion of listings** - **39%**. This **validates my reasoning** that Hanoi and Ho Chi Minh City are the 2 most crowded cities in Vietnam with extremely high housing demand and higher housing supply compared to other regions. Notably, the number of listings in Hanoi alone is equivalent to **80%** of the **combined listings** from all other cities while Ho Chi Minh City **surpasses** other cities by **20%**.
2. **Average House Prices** in **Hanoi** and **Ho Chi Minh City** are also **markedly higher** than other cities as well: **6.21** for HCM City, **6.15** for Hanoi, **5.00** for Others. **Fully furnished** houses **understandably** have the **highest average price** compared to Partially furnished and Unfurnished houses in all three regions.
3. Due to being **densely populated**, both **Hanoi** and **HCM City** have **significantly lower Average House Area** (**43.97** and **66.00**, respectively) in comparision with other cities (**104.36 square meters!**).
4. However, due to the **expensiveness** of both **Hanoi** and **HCM City**, they have **much higher** **Median Price per Square Meter** than other cities: **0.149**, **0.100** and **0.051**, respectively.
5. **Drilling through** the bar chart allows us to **dig deeper** into houses with **different bedrooms configuration**. Houses with **3 bedrooms** and **legally certified** has the **highest** total number of listings, at **7.5k**, which tells us the **preferences** of **Vietnamese** people.








