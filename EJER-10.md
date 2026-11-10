## Ejercicio 10: Patrón de letras

**Responsable:** [Nombre] · **Revisor (PR):** [Nombre]

---

### A · Enunciado

Dado n por teclado, imprima el siguiente patrón de letras.

**Ejemplo:** n = 5.

```
A
BA
CBA
DCBA
EDCBA
```

Se debe usar la notación ABI para los registros, mostrar mensajes claros al pedir los datos y resolverlo con un bucle doble.

---

### B · Código desarrollado

**Archivo:** `ej10.asm`

```asm
.data
    msg_n: .asciz "Ingrese n (1 a 26): "
    msg_error: .asciz "Error: n debe estar entre 1 y 26.\n"
    salto: .asciz "\n"

.text
.globl main
main:
    # Leemos n
    li a7, 4
    la a0, msg_n
    ecall

    li a7, 5
    ecall
    mv s0, a0

    # Validamos que n este entre 1 y 26
    li t2, 1
    blt s0, t2, error

    li t2, 26
    bgt s0, t2, error

    # Linea en blanco antes del patron
    li a7, 4
    la a0, salto
    ecall

    # Bucle de filas
    li t0, 0
filas:
    bge t0, s0, fin

    # Primera letra de la fila: 'A' + numero de fila
    li t1, 'A'
    add t1, t1, t0

    # Bucle de letras (de la mayor hasta la A)
letras:
    li a7, 11
    mv a0, t1
    ecall

    li t2, 'A'
    beq t1, t2, fin_fila

    addi t1, t1, -1
    j letras

    # Salto de linea al terminar cada fila
fin_fila:
    li a7, 11
    li a0, '\n'
    ecall

    addi t0, t0, 1
    j filas

    # Mensaje de error
error:
    li a7, 4
    la a0, msg_error
    ecall

    # Fin del programa
fin:
    li a7, 10
    ecall
```

---

### C · Explicación del procedimiento

Primero mostré un mensaje con `ecall 4`, leí n con `ecall 5` y lo guardé en `s0` con `mv`. Como el alfabeto solo tiene 26 letras, validé con `blt` y `bgt` que n estuviera entre 1 y 26. Si no lo está, el programa muestra un mensaje de error y termina.

Para generar las letras aproveché que cada carácter es un número (su código ASCII, `'A'` = 65). El bucle externo usa `t0` como número de fila (i = 0, 1, 2, …). Cada fila empieza en la letra `'A' + i`, que calculé con `add t1, t1, t0`. Así la fila 0 empieza en A, la fila 2 en C, etc.

El bucle interno imprime la letra de `t1` con `ecall 11`. Si esa letra ya es `'A'`, sale con `beq`; si no, resta 1 con `addi t1, t1, -1` para pasar a la letra anterior (C → B → A). Al terminar cada fila imprimo un salto de línea, aumento `t0` y regreso con `j` al bucle externo. Por último, terminé el programa con `ecall 10`.

---

### D · Resultado esperado

```
Ingrese n (1 a 26): 5

A
BA
CBA
DCBA
EDCBA
```

**Comprobación:** Para n = 5 el patrón termina en la fila EDCBA. La ejecución en RARS confirmó esta salida. También se probó con n = 26 (última fila `ZYXWVUTSRQPONMLKJIHGFEDCBA`) y con n = 0 y n = 27, donde se muestra el mensaje de error.
