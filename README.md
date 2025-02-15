# Blinkit-Analysis

### To conduct a comprehensive analysis of Blinkit's sales performance, customer satisfaction, and inventory distribution to identify key insights and opportunities for optimization using various KPIs.


### Data Cleaning : 
After exploring and evaluating dataset we found that [Fat_Content] column has some rows where we have to replace 'LF' with 'Low Fat' and 'reg' has to replace with 'Regular'.

![Cleaning2](https://github.com/user-attachments/assets/39bfa4db-6a63-4ba9-bcb3-8300fc9b2330)


```sql
UPDATE blinkit_grocery_data
SET Fat_Content = 
	CASE 
	WHEN Fat_Content IN('low fat' , 'LF') THEN 'Low Fat'
        WHEN Fat_Content = 'reg' THEN 'Regular'
        ELSE Fat_Content
	END ;
```





```sql
SELECT * FROM blinkit_grocery_data ;
```

## DATA ANALYSIS :

```sql
SELECT * FROM blinkit_grocery_data ;
```

![1](https://github.com/user-attachments/assets/f6254619-29ec-4dae-9cbc-39b6eb5350c9)


## KPI’s Requirements :

- 1). Total Sales: The overall revenue generated from all items sold.
 ```sql
SELECT SUM(Total_Sales) AS Total_Revenue FROM  blinkit_grocery_data ;
```

![2](https://github.com/user-attachments/assets/309c0e40-ce2a-4428-a49f-3f6fe6091765)


- 2). Average Sales: The average revenue per sale.

```sql
SELECT ROUND( AVG(Total_Sales) , 2 ) AS Avg_Revenue FROM  blinkit_grocery_data ;
```

![3](https://github.com/user-attachments/assets/a562bb63-2ab6-4007-9af0-7533d40f6f4d)

- 3). Number of Items: The total count of different items sold.
```sql
SELECT 
	COUNT(*) AS Count_Of_Items
FROM  blinkit_grocery_data
```

![4](https://github.com/user-attachments/assets/ae1d13fb-70d7-4bf0-9146-fce35b621123)


- 4). Average Rating: The average customer rating for items sold.

```sql
  SELECT ROUND( AVG(Rating) , 2 ) AS Avg_Rating 
  FROM blinkit_grocery_data ;
```

![5](https://github.com/user-attachments/assets/e0024438-3fe0-4d1d-a549-e2914330730f)


### Granular Requirements : 

- 1). Total Sales by Fat Content:
- Objective: Analyze the impact of fat content on total sales.
```sql
SELECT Fat_Content ,
	SUM(Total_Sales) AS Total_Sales
FROM blinkit_grocery_data 
GROUP BY Fat_Content 
ORDER BY Total_Sales DESC ;
```

![6](https://github.com/user-attachments/assets/c2778ee3-cd5a-4ada-bef6-6da45862dd86)

- 2). Total Sales by Item Type:
- Objective: Identify the performance of different item types in terms of total sales.
```sql
SELECT Item_Type ,
	CAST(SUM(Total_Sales) AS DECIMAL(10 , 2) ) AS Total_Sales
FROM blinkit_grocery_data 
GROUP BY Item_Type 
ORDER BY Total_Sales DESC ;
```

![7](https://github.com/user-attachments/assets/1f94e98b-522c-47a8-8560-849d2ca8a54f)

- 3). Fat Content by Outlet for Total Sales:
- Objective: Compare total sales across different outlets segmented by fat content.
  
```sql
SELECT Outlet_Location_Type, 
	SUM( CASE WHEN Fat_Content = 'Low Fat' THEN Total_Sales END ) AS Low_Fat ,
    SUM( CASE WHEN Fat_Content = 'Regular' THEN Total_Sales END ) AS Regular
FROM blinkit_grocery_data 
GROUP BY Outlet_Location_Type 
ORDER BY Outlet_Location_Type ;
```


![8](https://github.com/user-attachments/assets/6290c9cc-2ab1-42b1-a7de-8f60c0e2ab68)

- 4). Total Sales by Outlet Establishment:
- Objective: Evaluate how the age or type of outlet establishment influences total sales.

```sql
SELECT Outlet_Establishment_Year ,
	SUM(Total_Sales) AS Total_Sales
FROM blinkit_grocery_data 
GROUP BY Outlet_Establishment_Year
ORDER BY Outlet_Establishment_Year ;
```


![9](https://github.com/user-attachments/assets/7b8c9073-fbf7-4ddc-8ac4-70b7de4b9c6e)



- 5). Percentage of Sales by Outlet Size:
- Objective: Analyze the correlation between outlet size and total sales.

``sql
WITH cte AS (
	SELECT Outlet_Size , 
		SUM( Total_Sales ) AS Total_Sales 
	FROM blinkit_grocery_data  
	GROUP BY Outlet_Size
    )
SELECT Outlet_Size , Total_Sales ,
	(100*Total_Sales / SUM( Total_Sales ) OVER() ) AS Percentage_Sales
FROM cte ;
```


![10](https://github.com/user-attachments/assets/82436788-23a0-44e3-a3c6-ff13c351d184)

- 6). Sales by Outlet Location:
- Objective: Assess the geographic distribution of sales across different locations.

```sql
SELECT Outlet_Location_Type , 
	SUM(Total_Sales) AS Total_Sales
FROM blinkit_grocery_data 
GROUP BY Outlet_Location_Type
ORDER BY Outlet_Location_Type DESC;
```


![11](https://github.com/user-attachments/assets/adf6d64b-470a-408c-89ee-76ed7f93daad)


- 7). All Metrics by Outlet Type:
- Objective: Provide a comprehensive view of all key metrics (Total Sales, Average Sales, Number of Items, Average Rating) broken down by different outlet types.

```sql
SELECT Outlet_Type ,
	SUM(Total_Sales) AS Total_Sales,
	AVG(Total_Sales) AS Avg_Sales,
	COUNT(*) AS No_Of_Items,
	AVG(Rating) AS Avg_Rating,
	CAST(AVG(Item_Visibility) AS DECIMAL(10,2)) AS Avg_Item_Visibility
FROM blinkit_grocery_data 
GROUP BY Outlet_Type ;
```

![12](https://github.com/user-attachments/assets/e389a38c-5b1e-4dc8-8265-76d52a4d7457)

   

























