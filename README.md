CREATE TABLE `shop`.`products` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(45) NOT NULL,
  `cost` DECIMAL(7,2) NULL,
  PRIMARY KEY (`id`));
  
CREATE TABLE `shop`.`couriers` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(45) NOT NULL,
  `phoneNumber` VARCHAR(20) NOT NULL,
  `carBrand` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`id`));

CREATE TABLE `shop`.`orders` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `FIO_customer` VARCHAR(45) NOT NULL,
  `delivery_address` VARCHAR(45) NOT NULL,
  `courier_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `orders_couriers_idx` (`courier_id` ASC) VISIBLE,
  CONSTRAINT `orders_couriers`
    FOREIGN KEY (`courier_id`)
    REFERENCES `shop`.`couriers` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);
    
CREATE TABLE `shop`.`order_items` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `product_id` INT NOT NULL,
  `order_id` INT NOT NULL,
  `amount` INT NULL,
  PRIMARY KEY (`id`),
  INDEX `products_order_items_idx` (`product_id` ASC) VISIBLE,
  INDEX `orders_order_items_idx` (`order_id` ASC) VISIBLE,
  CONSTRAINT `products_order_items`
    FOREIGN KEY (`product_id`)
    REFERENCES `shop`.`products` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `orders_order_items`
    FOREIGN KEY (`order_id`)
    REFERENCES `shop`.`orders` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);
    
INSERT INTO `shop`.`products` (`name`, `cost`) VALUES ('Растишка', '90');
INSERT INTO `shop`.`products` (`name`, `cost`) VALUES ('Меч', '50');
INSERT INTO `shop`.`products` (`name`, `cost`) VALUES ('Торт', '800');
INSERT INTO `shop`.`products` (`name`, `cost`) VALUES ('Круасан', '70');
INSERT INTO `shop`.`products` (`name`, `cost`) VALUES ('Картошка фри', '150');

INSERT INTO `shop`.`couriers` (`name`, `phoneNumber`, `carBrand`) VALUES ('Джамшут', '+79999999999', 'Жигули');
INSERT INTO `shop`.`couriers` (`name`, `phoneNumber`, `carBrand`) VALUES ('Вова', '+75555555555', 'Приора');
INSERT INTO `shop`.`couriers` (`name`, `phoneNumber`, `carBrand`) VALUES ('Эрик', '+78888888888', 'Мерседес');

INSERT INTO `shop`.`orders` (`FIO_customer`, `delivery_address`, `courier_id`) VALUES ('Иосиф', 'Московская', '3');
INSERT INTO `shop`.`orders` (`FIO_customer`, `delivery_address`, `courier_id`) VALUES ('Рамиль', 'Цоколаева', '2');
INSERT INTO `shop`.`orders` (`FIO_customer`, `delivery_address`, `courier_id`) VALUES ('Лана', 'Леваневского', '1');
INSERT INTO `shop`.`orders` (`FIO_customer`, `delivery_address`, `courier_id`) VALUES ('Вероника', 'Киевская', '3');
INSERT INTO `shop`.`orders` (`FIO_customer`, `delivery_address`, `courier_id`) VALUES ('Роза', 'Шмулевича', '3');

INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('1', '1', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('4', '1', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('3', '1', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('2', '2', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('3', '2', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('4', '2', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('1', '3', '6');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('2', '3', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('1', '4', '1');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('5', '4', '3');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('2', '5', '2');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('1', '5', '1');

1)
SELECT o.fio_customer, o.delivery_address, c.name, p.name, p.cost, oi.amount, p.cost * oi.amount as Sum
FROM shop.orders as o

join shop.couriers as c
on o.courier_id = c.id

join shop.order_items as oi
on o.id = oi.order_id

join shop.products as p
on p.id = oi.product_id

where o.id = 1


2)
INSERT INTO `shop`.`orders` (`FIO_customer`, `delivery_address`, `courier_id`) VALUES ('Игнат', 'Зортова', '2');
INSERT INTO `shop`.`order_items` (`product_id`, `order_id`, `amount`) VALUES ('3', '6', '3');

3)
SELECT o.FIO_customer, o.delivery_address
FROM shop.orders as o

join shop.couriers as c
on o.courier_id = c.id

where c.id = 3
