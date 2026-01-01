# 🐍 Python - Diccionarios

## 📋 Contenido

* Diccionarios en Python: Concepto y Propiedades Clave
* Acceso a Elementos del Diccionario (llaves y valores)
* Modificación de Elementos (Actualizar valores)
* Adición de Nuevos Elementos
* Eliminación de Elementos
* Iteración sobre Diccionarios
* Copiar Diccionarios
* Creación de un Diccionario a partir de dos Listas
* Ejemplos Prácticos
    * p105-estudiante (Gestión de datos)
    * p081-calificaciones (Cálculo de promedios)
    * p082-nombres y edades (Entrada de datos y promedios)
    * p083-conversion-medida (Conversión de unidades)
    * p084-conversion-moneda (Conversión de divisas)
    * p085-portafolio-acciones (Finanzas) 🆕
    * p086-matriz-dispersa (Matemáticas) 🆕
    * p087-calculo-interes-simple (Finanzas/Matemáticas) 🆕
    * p088-datos-ventas-anuales (Finanzas) 🆕
    * p089-sistema-ecuaciones-lineales (Matemáticas) 🆕

***

## 🔑 Diccionarios en Python: Concepto y Propiedades Clave

* **Almacenamiento:** Los diccionarios se usan para almacenar valores en pares **llave:valor**.
* **Sintaxis:** Se crean usando llaves `{}` y especificando pares `llave:valor` separados por comas.
    * *Ejemplo:* `auto = { 'marca':'Ford', 'modelo':'Mustang', 'ano': 1964 }`
* **Propiedades Clave**:
    * **Ordenados:** Los elementos tienen un orden definido que no cambia (desde Python 3.7+).
    * **Modificables:** Es posible modificar, agregar o remover elementos después de su creación.
    * **No Duplicados:** No se permiten dos elementos con la misma llave. Una llave repetida sobrescribe el valor anterior.

***

## 🔍 Acceso a Elementos del Diccionario

* **Acceso por Llave (Sintaxis Estándar):** Refiriéndose al nombre de la llave entre corchetes `[]`.
    * *Ejemplo:* `m = auto['modelo']`
* **Acceso por Método `get()`:** Una alternativa que permite especificar un valor por defecto si la llave no existe.
    * *Ejemplo:* `auto.get('modelo')`
* **Obtener todas las Llaves:** Usando el método `keys()`. Devuelve una vista de las llaves.
    * *Ejemplo:* `k = auto.keys()`
* **Obtener todos los Valores:** Usando el método `values()`. Devuelve una vista de los valores.
    * *Ejemplo:* `v = auto.values()`

***

## ✍️ Modificación de Elementos (Actualizar valores)

* **Por Asignación Directa:** Utilizando el nombre de la llave y asignando un nuevo valor.
    * *Ejemplo:* `auto['ano'] = 2022`
* **Por Método `update()`:** Para actualizar uno o varios pares llave:valor simultáneamente.
    * *Ejemplo:* `auto.update({'ano':2022})`

***

## ➕ Adición de Nuevos Elementos

* **Por Asignación Directa:** Si la llave no existe, se añade el nuevo par llave:valor.
    * *Ejemplo:* `auto['color'] = 'blanco'`
* **Por Método `update()`:** También se puede usar para agregar nuevos elementos.
    * *Ejemplo:* `auto.update({'color':'blanco'})`

***

## 🗑️ Eliminación de Elementos

* **Método `pop()`:** Remueve el elemento asociado a una llave específica y devuelve su valor.
    * *Ejemplo:* `m = auto.pop('modelo')`
* **Método `popitem()`:** Remueve y devuelve el último par llave:valor insertado (o un par arbitrario en versiones antiguas de Python).
    * *Ejemplo:* `v = auto.popitem()`
* **Método `clear()`:** Elimina todos los elementos del diccionario, dejándolo vacío.
    * *Ejemplo:* `auto.clear()`

***

## 🔄 Iteración sobre Diccionarios

* **Iterar por Llaves:** Usando el método `keys()`.
    * *Ejemplo:* `for k in auto.keys(): print(k)`
* **Iterar por Valores:** Usando el método `values()`.
    * *Ejemplo:* `for v in auto.values(): print(v)`
* **Iterar por Llaves y Valores:** Usando el método `items()`, el cual devuelve pares (llave, valor).
    * *Ejemplo:* `for k,v in auto.items(): print(k, v)`

***

## 📑 Copiar Diccionarios

* **Método `copy()`:** Crea una copia superficial independiente del diccionario original.
    * *Ejemplo:* `otroauto = auto.copy()`
* **Función `dict()`:** También se puede usar para crear una copia del diccionario original.
    * *Ejemplo:* `otroauto = dict(auto)`

***

## 🔗 Crear Diccionario en base a dos Listas

* **Uso de `zip()` y `dict()`:** La función `zip()` combina las listas (llaves y valores) en pares de tuplas, que luego la función `dict()` convierte en un diccionario.
    * *Ejemplo:* `trabajador = dict(zip(llaves, valores))`

***

## 💻 Ejemplos Prácticos

### p105-estudiante: Gestión de Datos de un Estudiante

**Enunciado Mejorado:** Desarrolle un programa que cree un diccionario para almacenar la información de un estudiante (nombre, edad, email, carrera). Luego, actualice la información agregando la 'calificacion' y modificando el 'email'. Finalmente, imprima por separado las llaves, los valores, y ambos pares (llave:valor) del diccionario actualizado.

### p081-calificaciones: Análisis de Notas Académicas

**Enunciado Mejorado:** Utilice dos listas (`materias` y `calificaciones`) para crear un diccionario de notas. Demuestre las operaciones de agregar, eliminar y modificar entradas en el diccionario. Finalmente, recorra el diccionario para calcular y mostrar la suma y el promedio de las calificaciones.

### p082-nombres y edades: Registro Dinámico de Personas

**Enunciado Mejorado:** Cree un programa que solicite al usuario ingresar nombres y edades de manera interactiva, almacenando los datos en un diccionario. El ingreso finaliza cuando se introduce un nombre vacío. Al terminar, muestre el diccionario completo y calcule la suma y el promedio de todas las edades registradas.

### p083-conversion-medidas: Conversor de Longitud a Metros

**Enunciado Mejorado:** Defina un diccionario que almacene los factores de conversión a metros para diferentes unidades de longitud (`km`, `m`, `cm`, `mm`). Pida al usuario que ingrese una cantidad y una unidad, y use el diccionario para realizar y mostrar la conversión a metros.

### p084-conversion-moneda: Conversor de Divisas a Pesos Mexicanos (MXN)

**Enunciado Mejorado:** Implemente un conversor de divisas. Utilice un diccionario para almacenar las tasas de conversión de varias monedas (`USD`, `EUR`, `GBP`, `JPY`, `CAD`) a Pesos Mexicanos (MXN). Permita al usuario seleccionar una moneda y una cantidad, y muestre el resultado de la conversión.

***

## 📊 5 Ejemplos Adicionales (Finanzas y Matemáticas - Nivel Medio)

### p085-portafolio-acciones: Gestión de un Portafolio de Inversión (Finanzas)

**Enunciado:** Cree un diccionario para representar un portafolio de acciones, donde la llave es el símbolo de la acción (e.g., 'AAPL', 'GOOGL') y el valor es un diccionario anidado con su cantidad de *acciones* y su *precio_compra*. Calcule el **valor total invertido** en el portafolio.

```python
# p085-portafolio-acciones
portafolio = {
    'AAPL': {'acciones': 100, 'precio_compra': 150.00},
    'GOOGL': {'acciones': 50, 'precio_compra': 2500.00},
    'MSFT': {'acciones': 75, 'precio_compra': 300.00}
}
inversion_total = 0
for ticker, datos in portafolio.items():
    inversion_total += datos['acciones'] * datos['precio_compra']
print(f"El valor total invertido en el portafolio es: ${inversion_total:,.2f}")

```


```
auto = { 'marca':'Ford', 'modelo':'Mustang', 'ano': 1964 }
m = auto['modelo']
print(m) # Musang
```
