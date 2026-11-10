## Ejercicio 9: Rectángulo de asteriscos

**Responsable:** [Nombre] · **Revisor (PR):** [Nombre]

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

Primero mostré un mensaje con `ecall 4` y leí el número de filas con `ecall 5`. Como el valor leído queda en `a0` y ese registro se vuelve a usar en el siguiente `ecall`, lo copié a `s0` con `mv`. Hice lo mismo con el número de columnas y lo guardé en `s1`.

Después armé un bucle doble. El bucle externo usa `t0` como contador de filas y termina con `bge t0, s0, fin` cuando `t0` llega a f. Dentro de él, `t1` empieza en 0 en cada fila nueva y cuenta las columnas. Por cada columna imprimí un `*` con `ecall 11` y aumenté el contador con `addi`.

Cuando el bucle interno llega a c, imprimo un salto de línea (`'\n'`) con `ecall 11`, aumento `t0` y regreso con `j` al inicio del bucle externo. Por último, terminé el programa con `ecall 10`.

---

### D · Resultado esperado

```
Ingrese el numero de filas (f): 3
Ingrese el numero de columnas (c): 5

*****
*****
*****
```

**Comprobación:** Para f = 3 y c = 5 se esperan 3 filas de 5 asteriscos. La ejecución en RARS confirmó esta salida.
