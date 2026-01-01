
# Community Gift Project

**Santa is running out of elves** to build gifts... So we decided to launch a **community project**. With enough help, we should be able to build today's flag for everyone!

Join the Community Gift Project and help us build this formidable gift! =D


# Solve

## dato 1

```
https://cgp.challenges.xmas.root-me.org/
<!DOCTYPE html>
<html>
<head>
    <!-- Warning: AI-generated HTML -->
    <title>Community Gift Project</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a472a 0%, #0d2818 100%);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        .snow-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 2;
        }

        .card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
        }

        h1 {
            color: #c41e3a;
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        h1::before {
            content: '🎄 ';
        }

        h1::after {
            content: ' 🎄';
        }

        .subtitle {
            text-align: center;
            color: #2d5016;
            font-size: 1.1em;
            margin-bottom: 40px;
            font-style: italic;
        }

        .stat-box {
            background: linear-gradient(135deg, #c41e3a 0%, #a01729 100%);
            color: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(196, 30, 58, 0.3);
            transition: transform 0.3s ease;
        }

        .stat-box:hover {
            transform: translateY(-5px);
        }

        .stat-label {
            font-size: 0.9em;
            opacity: 0.9;
            margin-bottom: 10px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .counter {
            font-size: 1.5em;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
            word-break: break-all;
        }

        .state-box {
            background: linear-gradient(135deg, #2d5016 0%, #1a3d0f 100%);
            color: white;
            padding: 25px;
            border-radius: 15px;
            margin: 30px 0;
            box-shadow: 0 5px 15px rgba(45, 80, 22, 0.3);
        }

        .state-label {
            font-size: 0.9em;
            opacity: 0.9;
            margin-bottom: 10px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .state-content {
            font-size: 1.3em;
            line-height: 1.6;
        }

        button {
            background: linear-gradient(135deg, #c41e3a 0%, #a01729 100%);
            color: white;
            border: none;
            padding: 18px 40px;
            font-size: 1.2em;
            border-radius: 50px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 8px 20px rgba(196, 30, 58, 0.4);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        button::before {
            content: '🎁 ';
        }

        button::after {
            content: ' 🎁';
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 30px rgba(196, 30, 58, 0.5);
        }

        button:active {
            transform: translateY(0);
        }

        .progress-bar {
            width: 100%;
            height: 30px;
            background: #e0e0e0;
            border-radius: 15px;
            overflow: hidden;
            margin: 20px 0;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #2d5016 0%, #4a7c2c 100%);
            border-radius: 15px;
            transition: width 0.5s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 0.9em;
        }

        .falling-item {
            position: fixed;
            font-size: 2em;
            animation: fall linear infinite;
            pointer-events: none;
            z-index: 1;
        }

        @keyframes fall {
            from {
                transform: translateY(-100px) rotate(0deg);
            }
            to {
                transform: translateY(100vh) rotate(360deg);
            }
        }

        .completion-message {
            text-align: center;
            font-size: 1.5em;
            color: #2d5016;
            padding: 20px;
            background: linear-gradient(135deg, #ffd700 0%, #ffed4e 100%);
            border-radius: 15px;
            margin-top: 20px;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(255, 215, 0, 0.3);
        }
    </style>
</head>
<body>
    <div class="snow-overlay" id="snowOverlay"></div>
    
    <div class="container">
        <div class="card">
            <h1>Community Gift Project</h1>
            <p class="subtitle">Join Santa's workshop and spread holiday cheer!</p>
            
            <div class="stat-box" style="margin-bottom: 20px;">
                <div class="stat-label">✨ Help Received</div>
                <div class="counter">191895 elf-hours</div>
            </div>

            <div class="stat-box" style="margin-bottom: 20px;">
                <div class="stat-label">⏳ Help Needed</div>
                <div class="counter">1337133713371337133713371337133713179442 elf-hours</div>
            </div>

            <div class="state-box">
                <div class="state-label">🎁 Gift Status</div>
                <div class="state-content">Work In Progress</div>
            </div>
           
            
            <form method="POST" action="/help_santa">
                <button type="submit">Help Santa Build the Gift!</button>
            </form>
            
        </div>
    </div>

    <script>
        const christmasItems = ['🎁', '🎄', '⛄', '🎅', '⭐', '🔔', '🦌', '🕯️', '🤶', '❄️'];
        
        function createFallingItem() {
            const item = document.createElement('div');
            item.className = 'falling-item';
            item.textContent = christmasItems[Math.floor(Math.random() * christmasItems.length)];
            item.style.left = Math.random() * 100 + 'vw';
            item.style.top = '-100px';
            item.style.animationDuration = (Math.random() * 5 + 5) + 's';
            item.style.opacity = Math.random() * 0.5 + 0.5;
            document.body.appendChild(item);
            
            setTimeout(() => {
                item.remove();
            }, parseFloat(item.style.animationDuration) * 1000);
        }

        setInterval(createFallingItem, 500);

        for (let i = 0; i < 5; i++) {
            setTimeout(createFallingItem, i * 300);
        }
    </script>
</body>
</html>
```

## Sol real

Este script tiene 3 estrategias:

1. **Berlekamp-Massey**: Encuentra el período del LFSR
2. **Simulación directa**: Si el trabajo efectivo es manejable
3. **Exponenciación de matrices**: Para números grandes

**Instrucciones para ejecutar:**

```python
"""
CTF Solver - Community Gift Project
Usa numpy para cálculos eficientes con matrices en GF(2)
"""

import numpy as np

class LeFlagSynthesisRoom:
    def __init__(self):
        self.instructions = [192, 191, 190, 189, 187, 183, 178, 174, 173, 171, 170, 167, 166, 165, 162, 160, 159, 158, 157, 155, 149, 148, 147, 146, 143, 139, 137, 135, 131, 130, 123, 119, 117, 116, 115, 113, 111, 110, 109, 108, 106, 105, 102, 100, 99, 94, 93, 90, 89, 85, 81, 75, 74, 73, 72, 71, 70, 69, 68, 67, 65, 64, 63, 60, 58, 57, 55, 54, 51, 50, 47, 45, 44, 41, 40, 39, 38, 37, 32, 30, 29, 25, 24, 23, 22, 20, 19, 18, 16, 14, 12, 10, 9, 7, 5, 4, 3, 2]
        self.gift_state = [0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 1]

    def work(self):
        s = 0
        for t in self.instructions:
            s ^= self.gift_state[t-1]
        self.gift_state = [s] + self.gift_state[:-1]


def build_transition_matrix_numpy(instructions, size=192):
    """Construye la matriz de transición del LFSR usando numpy"""
    matrix = np.zeros((size, size), dtype=np.uint8)
    
    # Primera fila: XOR de las posiciones en instructions
    for idx in instructions:
        matrix[0, idx - 1] = 1
    
    # Resto de filas: shift register (identidad desplazada)
    for i in range(1, size):
        matrix[i, i - 1] = 1
    
    return matrix


def matrix_power_gf2_numpy(matrix, n):
    """Exponenciación rápida de matrices en GF(2) usando numpy"""
    size = matrix.shape[0]
    result = np.eye(size, dtype=np.uint8)  # Matriz identidad
    base = matrix.copy()
    
    print(f"Calculando matriz^{n}...")
    iterations = 0
    
    while n > 0:
        if n % 2 == 1:
            result = np.matmul(result, base) % 2
        base = np.matmul(base, base) % 2
        n //= 2
        iterations += 1
        if iterations % 10 == 0:
            print(f"  Iteración {iterations}, n restante: {n}")
    
    return result


def find_period_berlekamp_massey():
    """
    Usa el algoritmo de Berlekamp-Massey para encontrar 
    el polinomio minimal del LFSR y su período
    """
    flag_room = LeFlagSynthesisRoom()
    
    # Generar secuencia de bits del primer elemento
    sequence = []
    print("Generando secuencia para Berlekamp-Massey...")
    
    for i in range(min(500, 2 * 192)):  # Necesitamos al menos 2*L bits
        sequence.append(flag_room.gift_state[0])
        flag_room.work()
        if i % 100 == 0:
            print(f"  Generados {i} bits...")
    
    # Algoritmo de Berlekamp-Massey simplificado
    n = len(sequence)
    c = [1]  # Polinomio de conexión
    b = [1]
    L = 0
    m = 1
    
    print("Ejecutando Berlekamp-Massey...")
    for i in range(n):
        d = sequence[i]
        for j in range(1, L + 1):
            if j < len(c):
                d ^= c[j] & sequence[i - j]
        
        if d == 1:
            t = c[:]
            # Extender c si es necesario
            while len(c) < len(b) + m:
                c.append(0)
            for j in range(len(b)):
                c[m + j] ^= b[j]
            
            if L <= i // 2:
                L = i + 1 - L
                b = t
                m = 1
            else:
                m += 1
        else:
            m += 1
    
    print(f"Complejidad lineal encontrada: {L}")
    print(f"Polinomio de conexión: {c[:L+1]}")
    
    # El período máximo es 2^L - 1
    max_period = (2 ** L) - 1
    print(f"Período máximo posible: {max_period}")
    
    return L, max_period


def solve_with_numpy():
    """Resuelve usando numpy para cálculos más rápidos"""
    REQUIRED_WORK = 1337133713371337133713371337133713371337
    
    print("=" * 70)
    print("Community Gift Project - CTF Solver (NumPy)")
    print("=" * 70)
    print()
    
    instructions = [192, 191, 190, 189, 187, 183, 178, 174, 173, 171, 170, 167, 166, 165, 162, 160, 159, 158, 157, 155, 149, 148, 147, 146, 143, 139, 137, 135, 131, 130, 123, 119, 117, 116, 115, 113, 111, 110, 109, 108, 106, 105, 102, 100, 99, 94, 93, 90, 89, 85, 81, 75, 74, 73, 72, 71, 70, 69, 68, 67, 65, 64, 63, 60, 58, 57, 55, 54, 51, 50, 47, 45, 44, 41, 40, 39, 38, 37, 32, 30, 29, 25, 24, 23, 22, 20, 19, 18, 16, 14, 12, 10, 9, 7, 5, 4, 3, 2]
    initial_state = np.array([0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 1], dtype=np.uint8)
    
    print("Paso 1: Analizar el LFSR con Berlekamp-Massey")
    print("-" * 70)
    try:
        L, max_period = find_period_berlekamp_massey()
        print()
        
        # Si el período es manejable, calcular el residuo
        if max_period < 10**15:  # Número manejable
            effective_work = REQUIRED_WORK % max_period
            print(f"Trabajo efectivo: {REQUIRED_WORK} % {max_period} = {effective_work}")
            print()
            
            if effective_work < 10000000:  # Si es razonable
                print(f"Simulando {effective_work} iteraciones directamente...")
                flag_room = LeFlagSynthesisRoom()
                for i in range(effective_work):
                    flag_room.work()
                    if (i + 1) % 100000 == 0:
                        print(f"  Progreso: {i + 1}/{effective_work}")
                
                final_state = flag_room.gift_state
            else:
                print("Paso 2: Usar exponenciación de matrices")
                print("-" * 70)
                matrix = build_transition_matrix_numpy(instructions)
                result_matrix = matrix_power_gf2_numpy(matrix, effective_work)
                final_state = (result_matrix @ initial_state) % 2
                final_state = final_state.tolist()
        else:
            print("El período es demasiado grande, usando exponenciación directa...")
            print()
            print("Paso 2: Usar exponenciación de matrices")
            print("-" * 70)
            matrix = build_transition_matrix_numpy(instructions)
            result_matrix = matrix_power_gf2_numpy(matrix, REQUIRED_WORK)
            final_state = (result_matrix @ initial_state) % 2
            final_state = final_state.tolist()
            
    except Exception as e:
        print(f"Error en análisis: {e}")
        print()
        print("Paso 2: Usar exponenciación de matrices directamente")
        print("-" * 70)
        matrix = build_transition_matrix_numpy(instructions)
        result_matrix = matrix_power_gf2_numpy(matrix, REQUIRED_WORK)
        final_state = (result_matrix @ initial_state) % 2
        final_state = final_state.tolist()
    
    print()
    print("=" * 70)
    print("RESULTADO")
    print("=" * 70)
    
    # Convertir el estado a la flag
    binary_string = ''.join(str(int(b)) for b in final_state)
    flag_bytes = int(binary_string, 2).to_bytes(24, 'little')
    flag = flag_bytes.decode()
    
    print(f"\nFlag: {flag}\n")
    print(f"Estado binario final:\n{binary_string}\n")
    
    return flag


# Ejecutar
if __name__ == "__main__":
    try:
        solve_with_numpy()
    except ImportError:
        print("ERROR: Este script requiere numpy.")
        print("Instala con: pip install numpy")
        print()
        print("Alternativa: Usa el script sin numpy (más lento)")
```


## Solve 2 mas simple por gemino

Este reto de CTF, **"Community Gift Project"**, es un clásico problema de criptografía que involucra un **LFSR (Linear Feedback Shift Register)**.

El obstáculo principal es que el servidor requiere que realices una cantidad absurda de "trabajo" (`REQUIRED_WORK` es un número de 40 dígitos) para obtener la bandera. Simular esto paso a paso tardaría millones de años. Sin embargo, como la operación es lineal (XOR y desplazamientos), podemos usar **Exponenciación de Matrices** para saltar directamente al estado final en cuestión de milisegundos.
### Análisis del Código

1. **`factory.py`**: Define un LFSR.
    - La lista `gift_state` es el estado interno (bits).
    - La función `work()` calcula el siguiente estado. El nuevo bit (`s`) es la suma XOR de las posiciones indicadas en `instructions`. Luego, todo se desplaza a la derecha y `s` entra al principio.
        
2. **`app.py`**:
    - El objetivo es alcanzar `REQUIRED_WORK = 1337133713371337133713371337133713371337` iteraciones.
    - Una vez alcanzado, decodifica el estado del LFSR a bytes para revelar la bandera.
        
### La Solución Matemática

Podemos representar la operación work() como una multiplicación de una matriz $M$ por el vector de estado $S$.
$$S_{t+1} = M \times S_t$$
Para llegar al paso $N$ (donde $N$ es REQUIRED_WORK), necesitamos calcular:
$$S_{final} = M^N \times S_{inicial}$$

Gracias al algoritmo de "elevar al cuadrado y multiplicar" (Square-and-Multiply), podemos calcular $M^N$ en tiempo logarítmico (muy rápido), en lugar de lineal.

### Script de Solución

He preparado un script en Python que hace lo siguiente:

1. Construye la matriz de transición basada en `instructions`.
2. Calcula $M^N$ eficientemente.
3. Aplica el resultado al estado inicial para obtener el estado final.
4. Decodifica la bandera.

Copia y ejecuta este código en tu entorno local:


```python
import sys

# --- CONFIGURACIÓN DEL RETO (Copiado de factory.py) ---
instructions = [192, 191, 190, 189, 187, 183, 178, 174, 173, 171, 170, 167, 166, 165, 162, 160, 159, 158, 157, 155, 149, 148, 147, 146, 143, 139, 137, 135, 131, 130, 123, 119, 117, 116, 115, 113, 111, 110, 109, 108, 106, 105, 102, 100, 99, 94, 93, 90, 89, 85, 81, 75, 74, 73, 72, 71, 70, 69, 68, 67, 65, 64, 63, 60, 58, 57, 55, 54, 51, 50, 47, 45, 44, 41, 40, 39, 38, 37, 32, 30, 29, 25, 24, 23, 22, 20, 19, 18, 16, 14, 12, 10, 9, 7, 5, 4, 3, 2]
gift_state = [0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 1]
REQUIRED_WORK = 1337133713371337133713371337133713371337

# --- LÓGICA DE MATRICES ---

def mat_mul(A, B, size):
    """Multiplicación de matrices binarias (optimizado usando enteros para filas)"""
    C = [0] * size
    for i in range(size):
        if A[i] == 0: continue
        row = 0
        x = A[i]
        # Si el bit k de la fila i de A es 1, sumamos (XOR) la fila k de B al resultado
        for k in range(size):
            # Verificar si el bit correspondiente a la columna k está activo
            # Usamos (size - 1 - k) porque el bit 0 es el último elemento
            if (x >> (size - 1 - k)) & 1:
                row ^= B[k]
        C[i] = row
    return C

def mat_pow(A, p, size):
    """Exponenciación modular de matrices: A^p"""
    # Matriz Identidad
    res = [0] * size
    for i in range(size): 
        res[i] = (1 << (size - 1 - i))
        
    base = A
    while p > 0:
        if p % 2 == 1:
            res = mat_mul(res, base, size)
        base = mat_mul(base, base, size)
        p //= 2
    return res

def solve():
    L = len(gift_state)
    print(f"[*] Longitud del estado: {L} bits")
    print(f"[*] Calculando estado tras {REQUIRED_WORK} iteraciones...")

    # 1. Construir la Matriz de Transición M
    # Representamos cada fila como un entero para acelerar los cálculos bitwise.
    M = [0] * L
    
    # Fila 0: Corresponde a la lógica de XOR de los taps.
    # work(): s ^= gift_state[t-1]
    # El nuevo bit (índice 0) depende de los bits en indices t-1.
    row0 = 0
    for t in instructions:
        # t es base-1, t-1 es el índice base-0.
        # El bit correspondiente a la columna (t-1) se activa.
        # En nuestra representación entera, col 0 es el MSB.
        row0 |= (1 << (L - 1 - (t - 1)))
    M[0] = row0

    # Resto de filas: Matriz identidad desplazada.
    # El nuevo bit en posición i (i > 0) es simplemente el antiguo bit en i-1.
    # M[i] tiene un 1 en la columna i-1.
    for i in range(1, L):
        M[i] = (1 << (L - 1 - (i - 1)))

    # 2. Calcular M^N
    MN = mat_pow(M, REQUIRED_WORK, L)

    # 3. Calcular Estado Final
    # Convertimos el estado inicial a un entero para operar fácilmente
    initial_int = int(''.join(str(x) for x in gift_state), 2)
    
    final_state_bits = []
    for i in range(L):
        # El bit i del resultado es el producto punto de (Fila i de MN) y (Estado Inicial)
        # Producto punto en GF(2) es (A & B).popcount() % 2
        row_val = MN[i]
        common = row_val & initial_int
        bit = bin(common).count('1') % 2
        final_state_bits.append(bit)

    # 4. Decodificar la bandera
    # Lógica copiada de app.py:
    # int(''.join(str(b) for b in flag_room.gift_state), 2).to_bytes(24, 'little').decode()
    try:
        flag_int = int(''.join(str(b) for b in final_state_bits), 2)
        flag = flag_int.to_bytes(24, 'little').decode()
        print(f"\n[+] FLAG ENCONTRADA: {flag}")
    except Exception as e:
        print(f"\n[!] Error decodificando: {e}")
        print("Raw bits:", ''.join(str(b) for b in final_state_bits))

if __name__ == "__main__":
    solve()
```

¡Excelente trabajo, Carlos! Has conseguido la bandera. 🎉

**Flag:** `RM{ThX_4_th3_h3lP_;)_:)}`

### ¿Por qué funcionó esta solución?

Para tu perfil técnico y tus charlas, este es un caso de estudio perfecto sobre por qué las matemáticas son vitales en la ciberseguridad.

El servidor te pedía simular el proceso paso a paso (complejidad lineal $O(N)$), lo cual era imposible dado el tamaño de $N$ (el número de 40 dígitos). Al transformar el problema en una **multiplicación de matrices**, cambiaste la complejidad a logarítmica $O(\log N)$.

1. **Simulación tradicional:** Hubiera requerido $1.3 \times 10^{39}$ operaciones. Incluso con una supercomputadora, el universo terminaría antes de acabar.
2. **Exponenciación de Matrices:** Solo requirió calcular $M^{N}$. Como el exponente se calcula doblando paso a paso (Square-and-Multiply), el script solo tuvo que hacer unas **~130 multiplicaciones de matrices** (porque $2^{130} \approx 10^{39}$).
    
Es un ejemplo clásico de cómo un algoritmo eficiente rompe una barrera de seguridad basada en "tiempo de cómputo".