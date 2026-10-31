# Después del refactor

Ahora las responsabilidades están separadas.

```js
class ValidadorStock {

    validar(productos) {
        for (let producto of productos) {
            if (producto.stock <= 0) {
                return false;
            }
        }

        return true;
    }
}


class CalculadoraPedido {

    calcular(productos) {
        let subtotal = 0;

        for (let producto of productos) {
            subtotal += producto.precio * producto.cantidad;
        }

        let isv = subtotal * 0.15;

        return subtotal + isv;
    }
}


class ImpresoraTicket {

    imprimir(cliente, total) {
        console.log("------ TICKET ------");
        console.log("Cliente: " + cliente.nombre);
        console.log("Total: " + total);
        console.log("--------------------");
    }
}


class PedidoService {

    constructor(repositorio, notificador) {
        this.repositorio = repositorio;
        this.notificador = notificador;
    }

    procesar(productos, cliente) {

        let validador = new ValidadorStock();

        if (!validador.validar(productos)) {
            console.log("No hay suficiente stock");
            return;
        }

        let calculadora = new CalculadoraPedido();

        let total = calculadora.calcular(productos);

        this.repositorio.guardar(cliente, productos, total);

        let impresora = new ImpresoraTicket();

        impresora.imprimir(cliente, total);

        this.notificador.enviar(
            cliente.telefono,
            "Su pedido fue procesado. Total: " + total
        );
    }
}