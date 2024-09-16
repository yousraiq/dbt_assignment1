## dbt_assignment1
To address Fufu Republic's business needs, we can create a dimensional model that helps analyze sales trends, optimize inventory, and improve customer experience. Let’s go step by step:

## 1. Entities, Relationships, and Constraints

# Entities:
Branch: Represents each restaurant location (e.g., Lekki, Agege).
Attributes: Branch ID, Branch Name, Location, Manager
Menu Item: Represents the items sold in the restaurant (standardized core menu and branch-specific items).
Attributes: Item ID, Item Name, Category (e.g., main course, dessert), Price, Branch Availability
Customer: Represents customers who purchase from the restaurant.
Attributes: Customer ID, Name, Contact Info
Order: Represents each transaction.
Attributes: Order ID, Date, Time, Branch ID, Customer ID, Payment Method (Cash, POS, Online)
Order Line: Contains details of each item in the order.
Attributes: Order Line ID, Order ID, Item ID, Quantity, Price
Payment Method: Represents how customers pay for their orders.
Attributes: Payment Method ID, Type (Cash, POS, Online)
Inventory: Represents stock levels for each menu item.
Attributes: Item ID, Branch ID, Stock Level, Last Restocked Date

# Relationships:
A Branch has multiple Orders and manages its own Inventory of Menu Items.
A Customer can place multiple Orders, and each Order can contain multiple Order Lines (i.e., different menu items).
Each Order is associated with a Payment Method.

# Constraints:
Each Order must be linked to exactly one Branch and one Payment Method.
Inventory should be updated whenever an Order is placed.
Some menu items are specific to certain branches, so not all branches will stock every item.


## 2. Dimensional Model

# Business Process: 
Sales Analysis and Inventory Optimization

# Business Questions:
What are the sales trends across branches, payment methods, and dining options (dine-in, take-out, online)?
Which branches are running low on stock for certain menu items?
What are the top-selling items at each branch, and what payment methods are customers using most frequently?
How can promotions be tailored based on customer purchase history?

# Grain:
The grain of this fact table will be each individual order transaction. This gives us the ability to analyze sales at the most detailed level, such as specific menu items sold, the branch they were sold at, and how they were paid for.

# Dimensions:
Date Dimension: Tracks the day, month, and year of each sale.
Attributes: Date ID, Day, Month, Year, Weekday/Weekend
Branch Dimension: Stores information about each branch.
Attributes: Branch ID, Branch Name, Location
Menu Item Dimension: Stores details of each menu item sold.
Attributes: Item ID, Item Name, Category (e.g., Appetizer, Main Course), Price
Customer Dimension: Stores details of each customer (if customer tracking is implemented).
Attributes: Customer ID, Name, Contact Info
Payment Method Dimension: Tracks how the payment was made (Cash, POS, Online).
Attributes: Payment Method ID, Payment Type
Dining Option Dimension: Tracks whether the customer dined in, took out, or ordered online.
Attributes: Dining Option ID, Type (Dine-in, Take-out, Online)

# Fact:
Order Fact Table:
Grain: One row per order line item (i.e., an individual menu item sold in each order).
Measures: Quantity Sold, Total Sale Amount, Discount (if applicable).
Foreign Keys: Date ID, Branch ID, Item ID, Customer ID, Payment Method ID, Dining Option ID.


## 3. Insights 

This dimensional model allows Fufu Republic to:

Analyze sales trends by branch, item, payment method, and dining option.
Track inventory at each branch and restock items based on sales patterns.
Identify top-selling items and create targeted promotions based on customer purchase history.

## 4. ERD Diagram
![FUFU ERD Diagram](ERD(FUFU).png)