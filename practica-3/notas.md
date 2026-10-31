# Notas sobre los principios aplicados

## Principio [número de S] - Responsabilidad Única

Antes del refactor, la clase Pedido tenía varias responsabilidades al mismo tiempo.  
Validaba el stock, calculaba el total, guardaba el pedido, imprimía el ticket y enviaba mensajes.  
Después del cambio, cada responsabilidad quedó separada en una clase diferente.  
Esto hace que cada clase tenga una función más clara dentro del sistema.  
También facilita hacer cambios sin afectar otras partes del código.

## Principio [número de D] - Inversión de Dependencias

La clase PedidoService ya no crea directamente la conexión a la base de datos.  
Tampoco depende directamente del servicio que envía mensajes por WhatsApp.  
Ahora esas dependencias se reciben por medio del constructor.  
Esto permite cambiar la forma de guardar o notificar sin modificar PedidoService.  
También hace más fácil probar el sistema con otras implementaciones.