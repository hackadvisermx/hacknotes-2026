
### 💻 Planteamiento del Problema

Se desea procesar el inventario de productos de una tienda de electrónicos ("TecnoTienda"). Para ello, deberá solicitar al usuario los siguientes datos por cada producto:

- **nombre** (del producto)
    
- **precio** (valor numérico, ej. 1500.50)
    
- **categoria** (ej. 'Laptops', 'Celulares', 'Audio')
    
- **proveedor** (el nombre del distribuidor, ej. 'Sony', 'HP', 'Generico')
    
- **stock** (cantidad en inventario, ej. 25)
    

Los datos se deben almacenar en una **lista**, donde cada elemento de la lista sea un **diccionario** con los datos de un producto. 1

### 📊 Requisitos de Salida

Al terminar la captura (ej. cuando el usuario ingrese un nombre de producto vacío), el programa deberá procesar la lista e imprimir:

1. **Datos Crudos:** La lista de diccionarios tal como se almacenó. 2
    
2. **Formato Tabular:** Los datos de los productos organizados en una tabla clara. 3
    
3. **Resumen del Inventario:** Un resumen que incluya:
    
    - Total de productos registrados. 4
        
    - Cuántos productos por categoría.
        
    - Cuántos productos por proveedor.
        
    - La suma total del stock y el promedio de stock por producto.
        
    - La suma total de precios (considerando un solo precio por producto) y el precio promedio. 5
        
    - El nombre y precio del producto más caro y del más barato. 6
        

---

### 🚀 Ejemplo de Ejecución

TecnoTienda - Sistema de Inventario

Captura de datos de los productos (* para terminar):

... (Aquí iría la captura de datos) ...

**1. Datos (Lista de diccionarios):**

```
[{'nombre': 'Laptop Pro', 'precio': 32500.0, 'categoria': 'Laptops', 'proveedor': 'HP', 'stock': 15}, 
 {'nombre': 'Mouse Óptico', 'precio': 450.5, 'categoria': 'Accesorios', 'proveedor': 'Generico', 'stock': 50}, 
 {'nombre': 'Celular Z', 'precio': 18000.0, 'categoria': 'Celulares', 'proveedor': 'Samsung', 'stock': 25}, 
 {'nombre': 'Audífonos BT', 'precio': 1200.0, 'categoria': 'Audio', 'proveedor': 'Sony', 'stock': 30}]
```

**2. Tabla de datos:**

|**Nombre**|**Precio**|**Categoría**|**Stock**|**Proveedor**|
|---|---|---|---|---|
|Laptop Pro|32,500.00|Laptops|15|HP|
|Mouse Óptico|450.50|Accesorios|50|Generico|
|Celular Z|18,000.00|Celulares|25|Samsung|
|Audífonos BT|1,200.00|Audio|30|Sony|

**3. Resumen:**

Productos totales: 4

Categorías:

- Laptops: 1
    
- Accesorios: 1
    
- Celulares: 1
    
- Audio: 1
    
    Proveedores:
    
- HP: 1
    
- Generico: 1
    
- Samsung: 1
    
- Sony: 1
    
    Stock -> Suma: 120, Promedio: 30.0
    
    Precio -> Suma: 52,150.50, Promedio: 13,037.63
    
    Laptop Pro de 32,500.00 es el más caro, Mouse Óptico de 450.50 es el más barato.