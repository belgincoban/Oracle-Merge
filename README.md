# Oracle-Merge Senaryo Örneği

/*** Kaynak Tablo oluşturma scripti***/

CREATE TABLE PizzaMenu(
   PizzaId       number(7) NOT NULL,
   Name          VARCHAR2(30),
   Price         DOUBLE PRECISION,
   PizzaSize     VARCHAR2(10)
);


/*** Hedef Tablo oluşturma scripti***/

CREATE TABLE CopyPizzaMenu(
   PizzaId       number(7) NOT NULL,
   Name          VARCHAR2(30),
   Price         DOUBLE PRECISION,
   PizzaSize     VARCHAR2(10)
);

/** Tablolara örnek veri ekleme**/

INSERT INTO PizzaMenu (PizzaId,Name,Price,PizzaSize) VALUES 
	 (1, 'Pepperoni', 12.95, 'L'),
	 (2, 'Tonno',  11.49,    'L'),
	 (3, 'Hawaii', 9.69,    'L'),
	 (4, 'Vulcano', 11.95 ,  'L');

INSERT INTO CopyPizzaMenu (PizzaId,Name,Price,PizzaSize) VALUES 
	 (1, 'Pepperoniiii', 12.95, 'L'),
	 (2, 'Tonno',  11.49,    'L'),
	 (3, 'Hawaii', 10.69,    'XL');


/** Merge Kullanımı**/

merge into CopyPizzaMenu d
using PizzaMenu e
on (d.PizzaId=e.PizzaId)
when matched then
update set  d.name=e.name,d.price=e.price,d.PizzaSize=e.PizzaSize
when not matched then
	insert (PizzaId,Name,Price,PizzaSize)
	values (e.PizzaId, e.Name, e.Price, e.PizzaSize);
