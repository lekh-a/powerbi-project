This dataset contains sales transaction data from Blinkit, an online grocery delivery platform. It provides valuable insights into customer purchasing behavior, product demand, revenue trends, and sales performance over time
Dataset Overview :
- Contains sales data from Blinkit, including product details, order quantities, revenue, and Sales.
- Useful for demand forecasting, price optimization, trend analysis, and business insights.
- Helps in understanding customer behavior and seasonal variations in online grocery shopping.
- The dashboard provides a comprehensive view of Blinkit's sales performance, customer insights, product performance, and geographical representation. It is designed to offer actionable insights into key business metrics.
________________________________________
Data Source :
1.	I have downloaded this dataset from https://www.kaggle.com/datasets/akxiit/blinkit-sales-dataset
2.	Transform the data into Power Query Editor
3.	Data Cleaning : 
-	Check for Null values or Missing values
-	Converting Decimal Number data type into Fixed decimal Number datatype 
(Products = price, mrp
 			Orders = order_total
 			Order_items = unit_price
 			Marketing_performance = spend, revenue_generated, roas)
-	Removed empty cell/rows from the column reasons_if_delayed from delivery_performance table
4.	DAX Measures :
- Total Sales	Total Sales = SUM(order_items[quantity])
- Total Revenue	Total Revenue = SUMX('order_items',order_items[quantity] * order_items[unit_price])
- Total Quantity Sold	Total Quantity Sold = SUM(order_items[quantity])
- Total Order	Total Order = DISTINCTCOUNT(orders[order_id])
- Total Customers	Total Customers = DISTINCTCOUNT(customers[customer_id])
- RevenuePerCampaign	RevenuePerCampaign = SUMX(RELATEDTABLE(order_items), order_items[quantity] * order_items[unit_price])
- Prev Month Revenue	Prev Month Revenue = CALCULATE([Total Revenue],DATEADD(orders[order_date], -1, MONTH))
- Prev Month Order	Prev Month Order = CALCULATE([Total Order], DATEADD(orders[order_date],-1,MONTH))
- PartnerOnTime%	PartnerOnTime% =
DIVIDE(
COUNTROWS(FILTER('orders', 'orders'[delivery_status] = "On Time")),
COUNTROWS('orders')
)
- OnTimeDelivery%	OnTimeDelivery% =
DIVIDE(
COUNTROWS(FILTER('Orders', 'Orders'[delivery_status] = "On Time")),
COUNTROWS('Orders')
) * 100
- No. of Items	No. of Items = DISTINCTCOUNT(products[product_id])
- DelayedOrders	DelayedOrders = COUNTROWS(FILTER('Orders', 'Orders'[delivery_status] <> "On Time"))
- Count of Rating	Count of Rating = COUNT(customer_feedback[rating])
- Count of OrderId	Count of OrderId = COUNT(orders[order_id])
- Count of feedback_text	Count of feedback_text = COUNT(customer_feedback[feedback_text])
- Conversion Rate	Conversion Rate = DIVIDE(DISTINCTCOUNT(orders[customer_id]), SUM(marketing_performance[target_audience]))
- Avg Sales	Avg Sales = DIVIDE([Total Sales],[Total Order])
- Avg Rating	Avg Rating = AVERAGE(customer_feedback[rating])
- Avg Product Rating	Avg Product Rating = AVERAGE(customer_feedback[rating])
