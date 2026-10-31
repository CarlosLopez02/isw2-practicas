# Antes del refactor

```js
class Pedido {

    procesarPedido(productos, cliente) {

        let total = 0;

        for (let producto of productos) {

            if (producto.stock <= 0) {
                console.log("Producto sin stock");
                return;
            }

            producto.stock = producto.stock - 1;

            let subtotal = producto.precio * producto.cantidad;

            total = total + subtotal;
        }

        let isv = total * 0.15;

        total = total + isv;

        console.log("Total del pedido: " + total);

        let conexion = conectarBaseDatos();

        conexion.guardar({
            cliente: cliente.nombre,
            productos: productos,
            total: total
        });

        console.log("Pedido guardado en la base de datos");

        console.log("------ TICKET ------");
        console.log("Cliente: " + cliente.nombre);
        console.log("Total: " + total);
        console.log("--------------------");

        let mensaje = "Su pedido fue procesado. Total: " + total;

        enviarWhatsApp(cliente.telefono, mensaje);

        console.log("Mensaje enviado al cliente");
    }
}