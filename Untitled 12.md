
### Enfoque Humano

- Analizar el código `SafeOpener.java`.
- Identificar la función `openSafe` y la comparación.
- Ver la cadena hardcodeada: `cGwzYXMzX...`
- Reconocer el formato Base64.
- Usar un decodificador (ej. `base64 -d`) para obtener el password.

### Enfoque Centauro

- Subir el código Java al LLM.
- **Prompt:** "Analiza este código. ¿Cómo obtengo la contraseña para 'Sesame open'?"
- **IA:** "El programa compara tu entrada (codificada en Base64) con una cadena hardcodeada. La cadena es `...`."
- **Prompt:** "Decodifica esa cadena Base64."



### Enfoque Humano

- Nos dan un archivo `.class` (bytecode compilado).
- Opción 1: Usar un decompilador (JD-GUI, cfr) para revertir a código `.java` y analizarlo.
- Opción 2 (Más rápido): Usar el comando `strings` sobre el archivo.
- `$ strings SafeOpener.class`
- El flag suele estar visible como una constante de texto plano dentro del binario.

### Enfoque Centauro

- Subir el archivo `.class` al LLM.
- **Prompt:** "Este es un archivo .class compilado. ¿Puedes analizar su contenido en busca de pistas o el flag?"
- La IA escanea el contenido binario como si fuera texto.
- **IA:** "He encontrado una cadena de texto legible dentro del archivo que coincide con el formato del flag: `picoCTF{...}`."


### Enfoque Humano

- Descargar el `timer.apk`.
- Usar **'jadx'** o **'mobsf'** para decompilar el APK y obtener el código fuente Java/Kotlin.
- Manualmente, leer el código (ej. `MainActivity.java`).
- Buscar strings: "flag", "picoCTF", "key", etc.
- Rastrear la lógica de cualquier función de "timer" o listener de botón para ver dónde se esconde o cómo se genera el flag.

### Enfoque Centauro

- Humano decompila con **'jadx'** (la IA no puede ejecutar software).
- Copiar las clases Java/Kotlin relevantes y pegarlas en el LLM.
- **Prompt:** "Analiza este código Android decompilado. ¿Cómo encuentro el flag? Fíjate en la lógica del timer."
- La IA identifica la función clave (ej. una cuenta regresiva o una variable hardcodeada) y extrae el flag o la lógica, ahorrando tiempo de análisis manual.



### Enfoque Humano

- Analizar el código `picker-I.py`.
- Identificar la vulnerabilidad: **`eval(user_input + '()')`**.
- El servidor ejecuta cualquier nombre de función que se le pase.
- Buscar otras funciones definidas en el script.
- Encontrar la función **`win()`**.
- Introducir `win` como input. El servidor ejecutará `eval('win()')`.

### Enfoque Centauro

- Pegar el código `picker-I.py` en el LLM.
- **Prompt:** "Analiza este código. ¿Hay alguna vulnerabilidad que me dé un flag?"
- **IA:** "Sí, el script usa `eval()` en la entrada del usuario. Puedes llamar a la función `win()` para obtener el flag."
- **Prompt:** "¿Qué debo escribir?"
- **IA:** "Simplemente escribe `win`."




### Enfoque Humano

- El reto ahora usa **`pickle.loads()`** en la entrada.
- Saber que `pickle` es inseguro y permite RCE.
- Manualmente, crear una clase Python maliciosa.
- Usar la función **`__reduce__`** para que `pickle` ejecute un comando (ej. `os.system`).
- Serializar el objeto con `pickle.dumps()` y enviarlo.

### Enfoque Centauro

- **Prompt:** "Este nuevo script usa `pickle.loads` en mi input. ¿Es esto vulnerable?"
- **IA:** "Sí, es extremadamente vulnerable a RCE."
- **Prompt:** "Escribe un script de Python que cree un payload de `pickle` para RCE que ejecute `ls /`."
- **IA:** (Genera el script completo con `__reduce__` y `os.system`).



### Enfoque Humano

- Analizar el nuevo código `picker-II.py`.
- Notar que `eval()` sigue presente, pero hay una nueva función `filter()`.
- El filtro bloquea explícitamente la palabra "win".
- El objetivo ya no es llamar a `win()`, sino ejecutar código arbitrario que lea el flag.
- Input directo: `print(open('flag.txt', 'r').read())`

### Enfoque Centauro

- Pegar el nuevo código en el LLM.
- **Prompt:** "Han actualizado el script. Ahora filtra la palabra 'win'. ¿Cómo puedo saltar este filtro y leer 'flag.txt'?"
- **IA:** "El filtro es simple. Puedes evitar llamar a `win()` y en su lugar enviar el comando directo para leer el archivo."
- **Prompt:** "Dame el payload."
- **IA:** "Prueba esto: `print(open('flag.txt', 'r').read())`"