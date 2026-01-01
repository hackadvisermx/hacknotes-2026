
## Paso 1: Modelo de Datos y Lógica (POO)

### Prompt 1: El Modelo (Datos)
Crear una clase Estudiante que sea Serializable. Debe tener Nombre (string), Edad (Int), Peso (float), Correo (string), FechaNacimiento (DaTeTime), Sexo (String) (Masculino/Femenino), Promedio (float). Genera un constructor, todos los getters/setters y toString. No documentes ni comentarios código.

### Prompt 2: La Lógica (Proceso)

Crea una clase Utileria en Java, con tres métodos grabarDatos recibe como parámetro archivo (string) con el nombre del archivo a grabar, datos (ArrayList Estudiante), con los datos a grabar, que serialize la lista datos en el archivo. Otro método leerDatos que lee el archivo y regresa la lista deserializada, ambos maneja IOException y ClassNotFoundException.  Otro método inicializar, que cargue 5 estudiantes de ejemplo y regrese la lista cargada con los datos. No hay mensajes de salida en pantalla para las acciones. Los mensajes de error se mandan a la consola de depuración. No documentes el código. 

## Paso 2: El Prompt de la Interfaz (GUI)

### Prompt 3: La Vista

- Ahora crea una clase AppEstudiante para la GUI de Java, solo la interfaz, sin funcionalidad aún, solo el método main que muestre el diseño
- La GUI será con Java Swing (JFrame)
- Tendrá una barra de menus principal, Archivo y Ayuda, y submenus Archivo - Abrir, Archivo - Grabar, Archivo - Salir, Ayuda - Acerca de..
- En el JFrame, un JTable dentro de un JScroolPane para visualizar los datos
- Abajo añade un panel para los datos de entrada, crear JLabels y JTextField, JSpinner (FechaNacimiento,Edad), JComboBox (Sexo).
- En la parte inferior añade un panel de botones : 'Editar' 'Nuevo', 'Guardar','Anterior', 'Siguiente', 'Estadística'.  

## Paso 3: Conectando la Lógica  

## Prompt 4: Funcionalidad del menú

Ahora genera la siguiente funcionalidad
- Al iniciar la aplicación se inicializan los datos y se cargan en el JTable y se deshabilita el panel de datos.
- La opción Archivo - Abrir muestra un JFileChooser para elegir el archivo que contiene los datos, mostrar los datos cargados en el JTable.
- La opción Archivo - Guardar muestra un JFileChooser para elegir el archivo donde va a guardar, guardar los datos cargados en la Lista.
- La opción Ayuda - Acerca de .. , muestra un cuadro de dialogo con los datos del programador y la versión de la aplicación ["Aplicacion de Gestión de Estudiantes", "Version: 1.0", "Programador: Carlos Hector Castaneda Ramirez"]

## Paso 4: El Reto de Navegación

### Prompt 5: Funcionalidad de navegación

Agrega ahora la funcionalidad de navegación:
- Al hacer clic a un registro en JTable, mostrar los datos en el panel de datos.
- Al hacer clic en Editar, habilitar el panel de datos y permitir los cambios
- Al hacer clic en Nuevo, limpiar los campos y permitir capturar un dato nuevo
- Al hacer clic en Guardar, agregar el dato capturado a la lista
- Al hacer clic en Siguiente, avanzar al siguiente registro
- Al hacer clic en Anterior, retroceder al registro anterior
- Al hacer clic en Estadisticas, mostrar un dialogo con las siguientadisticas: Hombres, Mujeres, Promedio Edad, Media Promedios, El mas joven, El mas viejo, El de mayor y menor promedio.
- Habilitar y deshabilitar los botones  y panel de datos cuando sea pertinente para evitar acciones no deseadas. 









