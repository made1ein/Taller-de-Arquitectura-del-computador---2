# Ejercicio 7 – Serie de números alternados

**Responsable:** Madelein · **Revisor (PR):** Alejandra



## A · Enunciado

Pida un valor `n` y muestre los primeros `n` términos de la serie 1, 5, 7, 11, 13, 17, ... separados por espacio. Para `n = 6` la salida es: `1 5 7 11 13 17`.


## B · Código desarrollado

**Archivo:** `ej07.asm`

```assembly
.data
    prompt: .asciz "Ingrese el valor de n: "
    space:  .asciz " "

.text
.globl main
main:
    li a7, 4
    la a0, prompt
    ecall

    li a7, 5
    ecall
    mv s0, a0

    li t0, 1
    li t1, 0
    li t2, 4

bucle:
    beq t1, s0, fin

    li a7, 1
    mv a0, t0
    ecall

    li a7, 4
    la a0, space
    ecall

    add t0, t0, t2

    li t3, 6
    sub t2, t3, t2

    addi t1, t1, 1
    j bucle

fin:
    li a7, 10
    ecall
