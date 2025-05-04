CREATE SCHEMA Sales

CREATE TABLE Sales.Customers(

customer_id int  PRIMARY KEY IDENTITY(1,1),
first_name varchar(30) ,
last_name varchar(30) ,
phone varchar(20) ,
email varchar(30) ,
street varchar(20) ,
city varchar(20) ,
state varchar(20) ,
zip_code varchar(20) ,

)

CREATE TABLE Sales.Stores(

store_id int  PRIMARY KEY IDENTITY(1,1),
store_name varchar(30) ,
phone varchar(20) ,
email varchar(30) ,
street varchar(20) ,
city varchar(20) ,
state varchar(20) ,
zip_code varchar(20) ,

)


CREATE TABLE Sales.Staffs(

staff_id int  PRIMARY KEY IDENTITY(1,1),
first_name varchar(30) ,
last_name varchar(30) ,
phone varchar(20) ,
email varchar(30) ,
active varchar(20) ,
store_id int  REFERENCES Sales.Stores(store_id),
manager_id int  REFERENCES Sales.Staffs(staff_id)
)


CREATE TABLE Sales.Orders(

order_id int  PRIMARY KEY IDENTITY(1,1),
customer_id int  REFERENCES Sales.Customers(customer_id),
order_status varchar(30) ,
order_date date ,
required_date date ,
shipped_date date ,
store_id int  REFERENCES Sales.Stores(store_id),
staff_id int  REFERENCES Sales.Staffs(staff_id)
)

CREATE SCHEMA Production


CREATE TABLE Production.Categories(

category_id int  PRIMARY KEY IDENTITY(1,1),
category_name varchar(30) ,
)



CREATE TABLE Production.Brands(

brand_id int  PRIMARY KEY IDENTITY(1,1),
brand_name varchar(30) ,

)

CREATE TABLE Production.Products(

product_id int  PRIMARY KEY IDENTITY(1,1),
product_name varchar(30) ,
brand_id int  REFERENCES Production.Brands(brand_id),
category_id int  REFERENCES Production.Categories(category_id),
model_year int,
list_price decimal(6,2)

)

CREATE TABLE Production.Stocks(

store_id int  REFERENCES Sales.Stores(store_id),
product_id int  REFERENCES Production.Products(product_id),
quantity int,
PRIMARY KEY (store_id,product_id)

)

CREATE TABLE Sales.OrderItems(

order_id int REFERENCES Sales.Orders(order_id),
item_id int ,
product_id int  REFERENCES Production.Products(product_id),
quantity int,
list_price decimal(6,2),
discount decimal(6,2),
PRIMARY KEY(order_id,item_id)

)

