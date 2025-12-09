<img width="1169" height="827" alt="tourist arrivals x revenue accomodation and food services x czechia" src="https://github.com/user-attachments/assets/1e5d5a51-8548-4f32-8aff-da8f761cc132" />
<img width="1169" height="827" alt="environmental subsidies x EV registrations Spain" src="https://github.com/user-attachments/assets/8b299853-3f94-4a23-97ac-005662be68fd" />
<img width="1000" height="800" alt="top10 customers" src="https://github.com/user-attachments/assets/90009bc2-9350-4cbe-a7cf-fc13719e7bdd" />


Northwind e-commerce database:
Identify ten biggest customers


Source: 
northwind.db
https://github.com/microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs

Method:


# 1 PRELIMINARY
python

import pandas as pd

import sqlite3 as sql



# 2 CHECK TABLES, FIND PATTERNS

northwind=sql.connect(r'Desktop\northwind.db')

cursor=northwind.cursor()

tables=pd.read_sql_query('SELECT tbl_name FROM sqlite_master WHERE type="table"', northwind) 

print(tables) 

pd.read_sql_query('SELECT COUNT (*) FROM Territories', northwind)

cursor.execute('PRAGMA table_info (Customers)')

cursor.fetchall()


customers=pd.read_sql_query('SELECT * FROM Customers', northwind)

print(custoemers)





# 3  IDENTIFY COMMON COLUMNS: Customers.CustomerID, ContactName, Orders.OrderID, CustomerID, Order Details.UnitPrice, Quantity,OrderID


# 4 WRITE QUERY: multiply unit price with quantity, sum, join customer details and order details from Orders, Order Details, and Customers tables, group by customers, sort by amount spent

query=pd.read_sql_query('SELECT SUM ([Order Details].UnitPrice * [Order Details].Quantity) AS TotalSpent, Orders.CustomerID, Customers.ContactName FROM Customers INNER JOIN Orders ON Orders.CustomerID=Customers.CustomerID INNER JOIN [Order Details] ON [Order Details].OrderID=Orders.OrderID GROUP BY Orders.CustomerID, Customers.ContactName ORDER BY TotalSpent DESC', northwind)



# 5 EXPORT QUERY
top10=query.head(10)


top10.to_csv(r'Desktop/top10.csv')




