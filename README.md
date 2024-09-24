Iniciamos con la creación de la base de datos "supermercado" con sus respectivas tablas, las cuales fueron llamadas
"Clientes", "Factruras", "Productos" y "Ventas".

Creamos las llaves para su cardinalidad.

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
