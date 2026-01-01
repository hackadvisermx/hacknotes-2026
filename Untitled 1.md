**Planteamiento del problema:** Crear un sistema simple de punto de venta (POS) para un puesto de comida.

1. **Base de Conocimiento:** Definir un diccionario `menu` con los productos y sus precios.
    
2. **Mostrar Menú:** Mostrar al usuario los productos disponibles y sus precios, iterando sobre el diccionario.
    
3. **Tomar Orden:** Preguntar al usuario qué desea ordenar en un bucle.
    
    - Si el producto no está en el menú, informarle.
        
    - Si el producto existe, solicitar la **cantidad**.
        
4. **Validación:** Usar `try...except ValueError` para asegurar que la **cantidad** sea un número entero y positivo.
    
5. **Cálculo:** Almacenar la orden en un nuevo diccionario (el "carrito").
    
6. **Reporte Final:** Cuando el usuario termine de ordenar (ingresando "fin"), mostrar un recibo con el subtotal por producto y el total general de la compra.