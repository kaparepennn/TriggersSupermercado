Iniciamos con la creación de la base de datos "supermercado" con sus respectivas tablas, las cuales fueron llamadas
"Clientes", "Factruras", "Productos" y "Ventas".

Creamos las llaves para su cardinalidad.

Empexamos con la creación de los triggers:



DELIMITER //

CREATE TRIGGER act_venta

AFTER INSERT ON Ventas

FOR EACH ROW

BEGIN 

   INSERT INTO Venta (id_Venta, Cantidad)
   
   VALUES (NEW.id_Venta, NEW.Cantidad, CURDATE());
   
END; //



/*Creamos un trigger para calcular el valor de la factura incluyendo
el iva*/

DELIMITER //

Create trigger calcular_valor after update

on Facturas

for each row

begin
	insert into facturas (Id_Factura, Fecha, Cant_producto, Valor_Factura)
 	values (" ", " ", " ", new.Valor_Factura*0.19);

end //



/*Auditoria para determinar que usuario realizó determinada acción, 
en este caso, para ver que usuario realizó la venta y la fecha en que la
se realizó*/

DELIMITER //

Create trigger auditoria after update 

on Ventas for each row

begin

   insert into Ventas (id_venta, Cantidad, Usuario, Fecha)
   values (user(), user(), user(), now());

end//
