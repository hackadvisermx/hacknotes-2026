
Written by Juna Lee and Puhalenthi

I'm a very good planner, but my robotics competition really fried my brain! I remember eating something for the past few weeks but I just can't seem to remember what. Can you please help me? Here's my [schedule](https://docs.google.com/spreadsheets/d/152qYlpG-FRBdHEfemX1_zD6dX1y1BO2JVmlxRRTYhDM/edit?usp=sharing) for reference

## Solucion

- El archivo es una tabla de horarios con registros diarios por hora, donde cada fila representa un día desde el 6 de marzo y cada columna representa una franja horaria (de 00:00 a ~11:00).
- Quitando colores de fondo y color de fuente, aparece la vandera en formato visible aunque un poco desordenada



```
bcactf{Apple_pieS_Are_yuMMy}
```


```python
import pandas as pd

file_path = 'schedule.xlsx'

df = pd.read_excel(file_path, header=None)

letters = []
for r in range(df.shape[0]):
    for c in range(df.shape[1]):
        val = df.iat[r, c]
        if isinstance(val, str) and len(val) == 1:
            letters.append(val)

flag = ''.join(letters)
print("Extracted flag:", flag)
```