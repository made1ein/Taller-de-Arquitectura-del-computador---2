### Para el Ejercicio 8 (`EJER-8.md`):

```markdown
# Ejercicio 8 – Suma de números impares

**Responsable:** Madelein · **Revisor (PR):** Alejandra

---

## A · Enunciado

Sume solo los números impares que se ingresen por teclado. El programa deja de pedir números cuando se ingresa 0. Al final muestre la suma. Ejemplo: 3, 4, 5, 8, 7, 0 -> Suma = 15.

---

## B · Código desarrollado

**Archivo:** `ej08.asm`

```assembly
.data
    prompt: .asciz "Ingrese un numero (0 para terminar): "
    res:    .asciz "Suma = "

.text
.globl main
main:
    li s0, 0

bucle_impares:
    li a7, 4
    la a0, prompt
    ecall

    li a7, 5
    ecall
    mv t1, a0

    beqz t1, mostrar_suma

    andi t2, t1, 1
    beqz t2, bucle_impares

    add s0, s0, t1
    j bucle_impares

mostrar_suma:
    li a7, 4
    la a0, res
    ecall

    li a7, 1
    mv a0, s0
    ecall

    li a7, 10
    ecall
