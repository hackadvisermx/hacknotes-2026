
# bad-grades

Written by Lam To

Josh has terrible grades, figure out why!

Remember to wrap the final flag in 'bcactf{}'.

## Solucion

```bash
ME: JOSHUA RICHARDS
CLASS: 2025
GRADE LEVEL: 9

COURSE: AMERICAN LITERATURE I
INSTRUCTOR: LAMBERT TORRES


===========TRANSCRIPT | TRIMESTER 2===========
|ASSIGNMENT|                    |%|  |GRADE|
==============================================
----------------------------------------------
FINAL EXAM                      73      C
----------------------------------------------
CATCHER IN THE RYE ESSAY        31      F
----------------------------------------------
JOURNAL ENTRY #9                65      D
----------------------------------------------
JOURNAL ENTRY #8                33      F
----------------------------------------------
JOURNAL ENTRY #7                70      C-
----------------------------------------------
TO KILL A MOCKINGBIRD ESSAY     73      C
----------------------------------------------
JOURNAL ENTRY #6                49      F
----------------------------------------------
MIDTERM EXAM                    23      F
----------------------------------------------
JOURNAL ENTRY #5                43      F
----------------------------------------------
JOURNAL ENTRY #4                31      F
----------------------------------------------
THE GREAT GATSBY ESSAY          28      F
----------------------------------------------
JOURNAL ENTRY #3                61      D-
----------------------------------------------
JOURNAL ENTRY #2                53      F
----------------------------------------------
JOURNAL ENTRY #1                24      F
```

- Extract the scores, convert them from hex, wrap in the flag prefix, done:

https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=NzMgMzEgNjUgMzMgNzAgNzMgNDkgMjMgNDMgMzEgMjggNjEgNTMgMjQ

```
73 31 65 33 70 73 49 23 43 31 28 61 53 24

bcactf{s1e3psI#C1(aS$}


```