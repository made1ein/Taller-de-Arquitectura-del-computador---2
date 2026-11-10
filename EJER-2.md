
# Ejercicio 2: Nombre y edad

**Responsable:** D'alessandro · **Revisor (PR):** Madelein

---

## A · Enunciado

Desarrollar un programa que solicite el nombre y la edad de una persona. Luego debe mostrar en dos líneas los mensajes `Hola, <nombre>` y `El proximo año tendras <edad+1> años`.

Se debe utilizar una cadena (`ecall 8`), un entero (`ecall 5`), el salto de línea con carácter (`ecall 11`) y la impresión de cadenas y enteros, emplear registros con notación ABI y finalizar el programa utilizando `ecall`.

---

## B · Código desarrollado

**Archivo:** `ej02.asm`

```asm
.data
    msg_nombre: .asciz "Ingrese su nombre: "
    msg_edad:   .asciz "Ingrese su edad: "
    msg_hola:   .asciz "Hola, "
    msg_prox:   .asciz "El proximo año tendras "
    msg_anios:  .asciz " años"
    nombre:     .space 50

.text
.globl main
main:
    # Pedimos el nombre
    li a7, 4
    la a0, msg_nombre
    ecall

    # Leemos el nombre como cadena
    li a7, 8
    la a0, nombre
    li a1, 50
    ecall

    # Quitamos el salto de linea que deja ecall 8
    la t0, nombre
    li t2, 10
quitar_nl:
    lb t1, 0(t0)
    beqz t1, fin_quitar
    beq t1, t2, reemplazar
    addi t0, t0, 1
    j quitar_nl
reemplazar:
    sb zero, 0(t0)
fin_quitar:

    # Pedimos la edad
    li a7, 4
    la a0, msg_edad
    ecall

    # Leemos la edad y le sumamos 1
    li a7, 5
    ecall
    addi s0, a0, 1

    # Primera linea: Hola, <nombre>
    li a7, 4
    la a0, msg_hola
    ecall

    li a7, 4
    la a0, nombre
    ecall

    li a7, 11
    li a0, 10
    ecall

    # Segunda linea: El proximo año tendras <edad+1> años
    li a7, 4
    la a0, msg_prox
    ecall

    li a7, 1
    mv a0, s0
    ecall

    li a7, 4
    la a0, msg_anios
    ecall

    # Finalizamos el programa
    li a7, 10
    ecall
```

---

## C · Explicación del procedimiento

Primero declaré en la sección `.data` los mensajes con `.asciz` y un espacio de 50 bytes llamado `nombre` con `.space`, donde se guarda el texto que escribe el usuario. Luego mostré el mensaje `Ingrese su nombre: ` con `ecall 4` y leí el nombre con `ecall 8`, indicando en `a0` la dirección del espacio y en `a1` el máximo de caracteres.

Después pedí la edad con `ecall 4` y la leí con `ecall 5`. Le sumé 1 con `addi` y guardé el resultado en `s0`, porque el registro `a0` se sobrescribe con los siguientes `ecall`.

Para la primera línea imprimí `Hola, ` y luego el nombre, ambos con `ecall 4`, y agregué el salto de línea con `ecall 11`. Para la segunda línea imprimí `El proximo año tendras `, después el valor de `s0` con `ecall 1` y al final ` años`, finalmente, utilicé `ecall 10` para terminar la ejecución del programa.

---

## D · Resultado esperado

Para comprobar el funcionamiento del programa, ingresamos el nombre Ana y la edad 20.

```text
Ingrese su nombre: Ana
Ingrese su edad: 20
Hola, Ana
El proximo año tendras 21 años
```

**Comprobación:** El programa debe mostrar el saludo con el mismo nombre ingresado y la edad aumentada en 1, en este ejemplo se utiliza Ana con 20 años, pero también puede funcionar con otros nombres y edades.
