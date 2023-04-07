create database shop; #создание бд магазин

create table shop.product ( 
	Id int not null AUTO_INCREMENT,
	name VARCHAR(20),
	price int,
    primary key (Id)
);     #создание таблицы продуктов 

create table shop.order ( 
	Id INT not null AUTO_INCREMENT,
	firstName VARCHAR(20),
    lastName VARCHAR(20),
	address VARCHAR(20),
    cntProduct int ,
	courier_id INT,
	product_id INT,
    primary key (Id)
);     #создание таблицы заказов 

create table shop.courier ( 
	Id INT not null AUTO_INCREMENT,
	firstName VARCHAR(20),
    lastName VARCHAR(20),
    number INT,
    markCar INT,
    primary key (Id)
);     #создание таблицы курьера

insert into shop.product ( name,price) values ("велосипед", 1000); 
insert into shop.product (name,price) values ("веер", 100); 
insert into shop.product (name,price) values ("утюг", 10000); 
insert into shop.product (name,price) values ("слон", 1004000); 
insert into shop.product (name,price) values ("верблюд", 44000);   #заполнение таблицы продуктов 

insert into shop.order ( firstName,lastName, address, courier_id, product_id) values ("Ramil", "Mamedov", "Zortova 5",1,2); 
insert into shop.order ( firstName,lastName, address, courier_id, product_id) values ("Ramil", "Mamedov", "Zortova 5",2,3); 
insert into shop.order (firstName,lastName, address, courier_id, product_id) values ("Ramil", "Mamedov", "Zortova 5", 1, 3); 
insert into shop.order ( firstName,lastName, address, courier_id, product_id) values ("Ramil", "Mamedov", "Zortova 5",2 ,2 ); 
insert into shop.order ( firstName,lastName, address, courier_id, product_id) values ("Ramil", "Mamedov", "Zortova 5",3,3);  #заполнение таблицы заказов 

insert into shop.courier ( firstName,lastName, number,markCar) values ("Ramil", "Mamedov", 30003000, 300); 
insert into shop.courier ( firstName,lastName, number,markCar) values ("Ramil", "Mamedov", 30003000, 300); 
insert into shop.courier ( firstName,lastName, number,markCar) values ("Ramil", "Mamedov", 30003000, 300); #заполнение таблицы курьер 

1)

select l.name , g.firstName , g.lastName , s.address , l.price ,s.cntProduct
from shop.order as s

inner join shop.courier as g
on g.id = s.courier_id

inner join shop.product as l
on l.id = s.product_id

2)

insert into shop.order ( firstName,lastName, address, courier_id, product_id) values ("Ramil", "Mamedov", "Zortova 5",1,2); 

3)
select s.firstName, s.lastName, s.address  
from shop.order as s

inner join shop.courier as g
on g.id = s.courier_id
