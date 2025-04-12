# Excel Pizza Sales Dashboard and Analysis

## Key Objectives
The goal of this project is to analyze 2015 pizza sales data to uncover key business insights, identify sales trends, and evaluate performance across different categories, sizes, and time periods. By completely using Excel for extracting, cleaning, processing, and visualizing the data, we aim to provide actionable insights to optimize sales strategies, improve inventory management, and enhance customer satisfaction.

Dataset Link: https://raw.githubusercontent.com/PlainChild/Excel-Pizza-Sales-Dashboard/refs/heads/main/pizza_sales.csv 

### KPI's REQUIREMENT
To measure business performance, we need to calculate the following metrics:
1. Total Revenue Gained: Sum of all pizza orders price.
2. Total Orders Placed: Count of all pizza orders placed.
3. Total Pizzas Sold: Sum of pizza quantities sold across all orders.
4. Average Value Per Order: Total revenue / Total Orders.
5. Average Pizzas Per Order: Total Pizzas Sold / Total Orders.


### CHARTS REQUIREMENT
To better understand sales trends and customer preferences, we will create the following interactive dashboards:
1. Daily Trend for Total Orders:
A bar chart displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis. 

2. Hourly Trend for Total Orders:
A line chart illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.

3. Percentage of Sales by Pizza Category: 
A column chart shows the distribution of sales across different pizza categories. This chart will provide insights about the popularity of certain pizza and their contribution to overall sales.

4. Percentage of Sales by Pizza Size:
A donut chart represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales. 

5. 5 Best Sellers by Total Pizzas Sold:
A bar chart highlights the 5 best-selling pizzas based on the total number of pizzas sold. This chart will help us identify the most popular pizza options. 

6. 5 Worst Sellers by Total Pizzas Sold:
Timeline Slicer/ Filler
A bar chart showcases the 5 worst-selling pizzas based on the total number of pizzas sold. This chart will enable us to identify underperforming or less popular pizza options.

## Workflow 
1. Get Data From Text/CSV
![Image](https://github.com/user-attachments/assets/10b46cf5-db19-4de1-8b90-03a0d30d4c1b)

2. Data Cleaning
- Data deduplication
![Image](https://github.com/user-attachments/assets/12d1aba3-0a82-48d3-810f-27d1b51b08ea)
- Check missing data
![Image](https://github.com/user-attachments/assets/ed3150ce-14a8-4823-8943-b96b1d387790) 
- Check for inconsistencies value (by looking for typos, or two different value with the same meaning)
![Image](https://github.com/user-attachments/assets/d42bbedc-8a5d-464d-84ac-0f5158aef698) 
- It is requested to convert pizza_size value: M -> Medium; S->Small; L->Large; etc. So, replace previous value with new value for pizza_size.
![Image](https://github.com/user-attachments/assets/a7687e9d-4dbd-4974-8013-bc6578779de6)
- Since price is in K/kilos(thousand), create new column “price_in_rp”,  to show the price in Rupiah by multiplying total_price with 1000.
Formula=[@[total_price]]*1000
![Image](https://github.com/user-attachments/assets/9e72fe0a-5c60-43fc-b52d-a022f573bfae) 


3. Create Pivot Table
![Image](https://github.com/user-attachments/assets/356a9258-6bc7-4bd8-a89a-3beeb51b00d7)
4. Search each KPI
- Since the unique ID is pizza_id, not order_id, in order to find out KPI of Total Orders, create new column “order_count”. This will show the count of order_id with the same value. So if one order_id has five pizza_id, then it will return 5. Then, we use this value to divide 1, so when we sum order_count, it will show the count of order_id, which is one, not five. 
Formula= =1/COUNTIF(B:B;[@[order_id]])
![Image](https://github.com/user-attachments/assets/172639d9-2963-4a52-9da6-d34cffe46218) 
- Put sum of price_in_rp for KPI of Total Revenue, sum of order_count for KPI of Total Order, and sum of quantity for KPI of Total Pizzas on Values field. 
![Image](https://github.com/user-attachments/assets/c6ba963e-7a7c-4246-8075-a30e476fa957) 
- Then, sum of price_in_rp value divided by sum of order_count value for KPI of Average Value per Order, and sum of quantity value divided by sum of order_count value for KPI of Average Pizzas per Order.
![Image](https://github.com/user-attachments/assets/7618f7ff-b018-4327-9d06-8f5c35648a50) 

5. Create another Pivot Table for Daily and Hourly Sales charts
- To show day’s names instead of the date, create new column “order_day”  to extract day’s name from order_date. 
Formula=TEXT([@[order_date]];"dddd")
![Image](https://github.com/user-attachments/assets/d20f8c7b-6cb1-49cb-868e-9d1beed8b98a) 
- Put sum of oder_count in Value field and order_day in Rows field for Daily Sales Trend.
![Image](https://github.com/user-attachments/assets/cce0e00b-ac35-416c-a816-0f866ea441b6) 
- Create column chart for KPI of Daily Sales Trend based on pivot table above 
![Image](https://github.com/user-attachments/assets/d4b78839-6e66-4581-8475-8f2c5f889987) 
- Copy pivot table above and change order_day with order_time in Rows field for Hourly Sales Trend. 
![Image](https://github.com/user-attachments/assets/90e1301d-ec44-40e4-a6c7-3794ee754c62) 
- Create line chart for KPI of Hourly Sales Trend based on pivot table above.
![Image](https://github.com/user-attachments/assets/d4c356bd-feca-45c5-be96-fdfdec0a26af) 

6. Create another Pivot Table for Pizza Sales by Size and Category charts
- Put pizza_size on Rows field and sum of price_in_rp on Values field for Pizza Sales by Size.
![Image](https://github.com/user-attachments/assets/30277f7e-1006-4309-9cd9-d00c3d3dd1c8) 
- Copy pivot table above and change pizza_size with pizza_category in Rows field for Pizza Sales by Category
![Image](https://github.com/user-attachments/assets/9256cc3b-900b-4ad7-92bf-84e701c1b4fc) 
- Create column chart for each pivot table
![Image](https://github.com/user-attachments/assets/5837589d-3c26-4326-b5af-617c00a085fe) 

7. Create another Pivot Table for 5 Best and Worst Selling Pizza charts
- Put pizza_name on Rows field and sum of quantity on Values field.
![Image](https://github.com/user-attachments/assets/4c1189f9-5fa8-419e-9a1d-7bec54b242f0) 
- Filter the data with Value Filter Top 5 for 5 Best Selling Pizza.
![Image](https://github.com/user-attachments/assets/aa933ddd-e4ea-4159-beba-81e5baad3b3e) 
- Copy pivot table above and Filter the data with Value Filter Bottom 5 for 5 Worst Selling Pizza.
![Image](https://github.com/user-attachments/assets/e2ed0f9d-c0e8-4488-a468-7425e27fcab6) 
- Create bar chart for each pivot table
![Image](https://github.com/user-attachments/assets/4a53fe0e-b991-4833-87f6-9b69d5880d39) 

7. Click any pivot table and Insert Timeline Filter
![Image](https://github.com/user-attachments/assets/27f703d2-068d-4a30-986b-f506a8ef7d08) 
8. Copy all charts and timeline filter into the sheet for dashboard, then arrange the dashboard and design it.
![Image](https://github.com/user-attachments/assets/08680f6f-522c-46ef-bf99-155d2905073b) 

## Insights & Findings
1. For Daily Sales Trend, it can be seen the peak sales are around the end of weekdays or on thursday and friday.
2. For Hourly Sales Trend, it can be seen the peak sales are at noon or around lunch time, and around evening or afterwork hours.  
3. For pizza sales percentages by size, Large is the most sold pizzas size with contribution of more than 60% to the total revenue, followed by Medium with almost 25%.
4. For pizza sales percentages by category, Chicken and Supreme dominates sales contribution by more than 70%, Chicken with more than 40% and Supreme with around 30%.
5. For best selling pizzas, they are The Classic Deluxe Pizza with 2453 sold, and The Barbecue Chicken Pizza with 2432 sold.
6. For worst selling pizzas, they are The Brie Carre Pizza with only 490 sold, and The Mediterranian Pizza with only 934 sold
