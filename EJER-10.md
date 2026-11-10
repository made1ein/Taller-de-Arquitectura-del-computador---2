## Ejercicio 10: Patrón de letras

**Responsable:** Alonso · **Revisor (PR):** Luis

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

Primero pedí n con `ecall 4` y `ecall 5` y lo guardé en `s0`. Como solo hay 26 letras, puse una validación con `blt` y `bgt` para que n esté entre 1 y 26, si no está sale un mensaje de error

Para las letras usé que cada carácter en realidad es un número (su código ASCII), entonces `'A' + 1` es `'B'`, `'A' + 2` es `'C'` y así. Con eso, cada fila empieza en `'A'` más el número de fila (`add t1, t1, t0`), por eso la primera empieza en A, la segunda en B, etc

En el bucle de adentro imprimo la letra con `ecall 11` y le resto 1 con `addi t1, t1, -1` para ir hacia atrás hasta llegar a la A, ahí paro con `beq`. Después imprimo el salto de línea, paso a la siguiente fila y por último cierro con `ecall 10`

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

**Comprobación:** Con n = 5 la última fila tiene que ser EDCBA. La ejecución en RARS debe confirmar esta salida
