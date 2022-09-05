The Problem:

Three tables have been designed to manage orders to an online book store. Three tables will 
be created as follows:

  1. OrderList(orderid:INT (pk, auto increment), bookid:INT, orderername:VARCHAR(50), ordereraddress:VARCHAR(50),  quantity:INT, fulfilled:INT)
  
  2. StockList(bookid:INT (pk, auto increment), booktitle:VARCHAR(50), author:VARCHAR(50), quantityinstock:INT)
  
  3. BackOrderList(backorderid:INT (pk, autoincrement), orderid:INT, quantity:INT)


All incoming orders are recorded in OrderList. The orderid is auto incremented. The bookid, ordername, orderaddress and quantity as passed from a Python Script. The script collects these details from a user (command line)  and uses the pymysql library to connect and insert 
the data to the database. 

An insert to the OrderList invokes a trigger. The trigger first checks if there is sufficient stock for the bookid passed in the insert (by checking StockList’s quantityinstock for the book). If there is sufficient stock, the order is inserted, and the StockList quantityinstock record for the book is decremented by the quantity ordered. The order is marked fulfilled by inserting 1 into the OrderList’s fulfilled attribute for the order. 

If there is insufficient stock, then the order is inserted into OrderList, but fulfilled is set to 0. 
A record of the order is added to the BackOrderList to aid with stock resupply. 


Tasks: 
  1. Create a set of tables and sample data that allow the resulting Python and Trigger to be 
  tested. This should conform to the  table descriptions provided above. 
  
  2. Implement a Python script that uses the pymysql library to connect to and insert a row 
  to the OrderList table. The values inserted should be provided by the user. You can 
  assume that the user will provide valid values each time. 
  
  3. Implement an appropriate trigger that fulfils the rest of the transaction as described 
  above
