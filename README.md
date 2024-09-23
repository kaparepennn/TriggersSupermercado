DELIMITER //
CREATE TRIGGER act_venta
AFTER INSERT ON Ventas
FOR EACH ROW
BEGIN 
   INSERT INTO act_venta(id_Venta, Cantidad)
   VALUES (NEW.id_Venta, NEW.Cantidad, CURDATE());
END; //
