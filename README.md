# PixelVault Games – Arquitectura 4+1 con PlantUML

Laboratorio de Arquitectura de Software. Modela una tienda e-commerce de videojuegos con el **Modelo de 4+1 Vistas de Kruchten** en PlantUML y lo traduce a una aplicación web funcional (SPA en un solo archivo HTML).

## Contenido

| Archivo | Descripción |
|---|---|
| `arquitectura.puml` | Las 5 vistas en PlantUML: Casos de Uso, Lógica, Procesos, Desarrollo y Despliegue |
| `index.html` | Aplicación web final (HTML + CSS + JavaScript, sin dependencias externas) |
| `README.md` | Este documento |

## Cómo ejecutar la aplicación

1. Descarga `index.html`.
2. Ábrelo con doble clic en cualquier navegador moderno (Chrome, Edge, Firefox).
3. No requiere servidor, instalación ni conexión a internet.

## Cómo visualizar los diagramas

`arquitectura.puml` contiene 5 bloques `@startuml ... @enduml`, uno por vista.

- **Online:** pega un bloque a la vez en [plantuml.com](https://www.plantuml.com/plantuml).
- **VS Code:** instala la extensión *PlantUML*, abre el archivo y usa `Alt + D` para previsualizar.

## Vistas del modelo 4+1

| Vista | Tipo de diagrama | Qué representa |
|---|---|---|
| Escenarios (+1) | Casos de uso | Actores (Cliente, Vendedor, Administrador) y RF1 a RF4 |
| Lógica | Clases | `Producto`, `Cliente`, `Arriendo`, `Venta` y sus relaciones |
| Procesos | Secuencia | Verificación de stock y cálculo de multa por devolución tardía |
| Desarrollo | Componentes | Frontend, API Gateway, microservicios y base de datos |
| Física | Despliegue | Navegador, servidor Node.js/Express y PostgreSQL |

## Funcionalidades de la aplicación

- **Catálogo (RF1):** búsqueda y filtros por plataforma (PS5, Xbox, Switch, PC) y formato (Físico/Digital). Los productos físicos muestran su stock.
- **Carrito (RF2):** descuenta el stock al agregar productos físicos. Calcula subtotal, descuentos, IVA del 19% y total. Acepta el cupón `PIXEL10` (10%) y un crédito trade-in.
- **Arriendos (RF3):** tarifa de $2.000 por día y multa de $1.500 por cada día de atraso. Se pueden editar los días transcurridos para simular una devolución tardía.
- **Cliente VIP (RF4):** el interruptor del encabezado aplica 10% de descuento en arriendos y acumula 1 punto por cada $1.000 comprados.

## Reglas de negocio

| Concepto | Valor |
|---|---|
| IVA | 19% sobre (subtotal − descuentos) |
| Cupón de prueba | `PIXEL10` = 10% sobre el subtotal |
| Tarifa de arriendo | $2.000 por día (máximo 14 días) |
| Multa por mora | $1.500 por día de atraso |
| Descuento VIP en arriendos | 10% |
| Puntos VIP | 1 punto por cada $1.000 del total de la compra |

La tarifa de arriendo, los puntos y el cupón no vienen en la guía original; son valores definidos para el prototipo y se pueden modificar en las constantes al inicio del script de `index.html`.

## Correspondencia UML → código

| Vista Lógica (UML) | Código JavaScript |
|---|---|
| `Producto.verificarStock()` | `class Producto` → `verificarStock(cant)` |
| `Arriendo.calcularMulta(diasAtraso)` | `class Arriendo` → `calcularMulta(diasAtraso)` |
| `Venta.calcularImpuestos()` | `class Venta` → `calcularImpuestos()` |
| `Cliente.esVIP`, `Cliente.puntos` | `class Cliente` |

## Pruebas sugeridas

1. Agrega un producto con stock bajo (por ejemplo *Pro Controller*, stock 1) y comprueba que se bloquea al agotarse.
2. En el carrito, ingresa el cupón `PIXEL10` y verifica el IVA y el total.
3. Registra un arriendo de 3 días, sube los días transcurridos a 5 y comprueba una multa de $3.000.
4. Activa el modo VIP, registra otro arriendo y comprueba el 10% de descuento.
5. Finaliza una compra con el modo VIP activo y verifica que se sumen puntos.

## Entregables del laboratorio

Carpeta comprimida `G4_Apellido_Nombre.zip` con:

1. Informe en PDF con la explicación de cada vista, capturas de los diagramas, los prompts exactos usados y capturas de la web.
2. `arquitectura.puml` con las 5 vistas.
3. `index.html` con la aplicación operativa.
