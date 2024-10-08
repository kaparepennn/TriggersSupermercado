Iniciamos con la creación de la base de datos "supermercado" con sus respectivas tablas, las cuales fueron llamadas
"Clientes", "Factruras", "Productos" y "Ventas".

![image](https://github.com/user-attachments/assets/9cbaa523-2839-4dcf-8406-faa4aef3f0da)

Creamos las llaves para su cardinalidad.

![image](https://github.com/user-attachments/assets/a35152b7-a94f-4e25-9db4-b585c441a8ec)
![image](https://github.com/user-attachments/assets/90d10bf9-e7fc-49bd-8737-e78fef91d54a)

Empezamos con la creación de los triggers:


/*Creamos un trigger para calcular el valor de la factura incluyendo
el iva*/

DELIMITER //

Create trigger calcular_valor after update

on Ventas

for each row

begin
	insert into facturas (Id_Factura, Fecha, Cant_producto,
    	Valor_Factura)
    	values (new.Id_Factura(), now(), new.Cant_producto(), 
    	new.Valor_Factura());

end //


/*Auditoria para determinar que usuario realizó determinada acción, 
en este caso, para ver que usuario realizó la venta y la fecha en que la
se realizó*/

DELIMITER //

Create trigger auditoria after update 

on facturas for each row

begin
	insert into Ventas (id_venta, Cantidad, Usuario, Fecha)
	values (new.id_venta(), new.Cantidad(), user(), now());

end//
