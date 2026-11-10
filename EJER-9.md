## Ejercicio 9: Rectángulo de asteriscos

**Responsable:** Alonso · **Revisor (PR):** Alejandra

---

### A · Enunciado

Lea dos números f y c, y dibuje un rectángulo de asteriscos de f filas y c columnas.

**Ejemplo:** f = 3, c = 5.

Se debe usar la notación ABI para los registros, mostrar mensajes claros al pedir los datos y resolverlo con un bucle doble.

---

### B · Código desarrollado

**Archivo:** `ej09.asm`

```asm
.data
    msg_f: .asciz "Ingrese el numero de filas (f): "
    msg_c: .asciz "Ingrese el numero de columnas (c): "
    salto: .asciz "\n"

.text
.globl main
main:
    # Leemos el numero de filas
    li a7, 4
    la a0, msg_f
    ecall

    li a7, 5
    ecall
    mv s0, a0

    # Leemos el numero de columnas
    li a7, 4
    la a0, msg_c
    ecall

    li a7, 5
    ecall
    mv s1, a0

    # Linea en blanco antes del dibujo
    li a7, 4
    la a0, salto
    ecall

    # Bucle de filas
    li t0, 0
filas:
    bge t0, s0, fin

    # Bucle de columnas
    li t1, 0
columnas:
    bge t1, s1, fin_fila

    li a7, 11
    li a0, '*'
    ecall

    addi t1, t1, 1
    j columnas

    # Salto de linea al terminar cada fila
fin_fila:
    li a7, 11
    li a0, '\n'
    ecall

    addi t0, t0, 1
    j filas

    # Fin del programa
fin:
    li a7, 10
    ecall
```

---

### C · Explicación del procedimiento

Primero pedí las filas y las columnas con `ecall 4` para el mensaje y `ecall 5` para leer el número. Cada valor lo pasé a `s0` y `s1` con `mv`, porque si lo dejaba en `a0` se me borraba con el siguiente `ecall`

Luego hice dos bucles, uno dentro del otro. El de afuera va contando las filas con `t0` y el de adentro las columnas con `t1`, que vuelve a 0 cada vez que empieza una fila nueva. En el de adentro voy imprimiendo un `*` con `ecall 11` hasta llegar a c

Cuando se completa la fila, imprimo un salto de línea, le sumo 1 a `t0` y regreso con `j` para hacer la siguiente fila, así hasta llegar a f. Al final cierro el programa con `ecall 10`

---

### D · Resultado esperado

```
Ingrese el numero de filas (f): 3
Ingrese el numero de columnas (c): 5

*****
*****
*****
```

**Comprobación:** Con f = 3 y c = 5 tienen que salir 3 filas de 5 asteriscos. La ejecución en RARS debe confirmar esta salida
