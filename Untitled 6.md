### Diapositiva 10: Leyendo un Archivo de Texto

Es el proceso inverso a la escritura y usa una lógica de anidamiento similar:

1. **`FileReader`:** La clase base. Se conecta al `File` para leer _caracteres_.
    
2. **`BufferedReader`:** El "envoltorio" (Wrapper) que se pone sobre `FileReader`.
    
    - **Beneficio 1:** Añade un búfer para leer eficientemente (lee "tramos" grandes del archivo, no carácter por carácter).
        
    - **Beneficio 2:** Nos da el método súper útil `readLine()`, que lee una línea completa de texto hasta encontrar un salto de línea.
        

- **Uso combinado:** `new BufferedReader(new FileReader(arch))`