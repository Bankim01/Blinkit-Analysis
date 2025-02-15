# blinkit-Analysis

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























