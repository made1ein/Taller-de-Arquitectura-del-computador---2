# Ejercicio 4: Operaciones con datos ingresados

**Responsable:** Madelein · **Revisora (PR):** Alonso

---

## A · Enunciado

Desarrollar un programa que solicite al usuario los valores de a, b, c y d para calcular la siguiente expresión:

`f = (5a + 2b + c) - (4d - 3)`

Se deben ingresar los cuatro valores por teclado, realizar las operaciones respetando los paréntesis y sin simplificar la expresión. Finalmente, guardar el resultado en un registro y mostrarlo en consola con el mensaje `f = `.

---

## B · Código desarrollado

**Archivo:** `ej04.asm`

```asm
.data
    msg_a: .asciz "Ingrese a: "
    msg_b: .asciz "Ingrese b: "
    msg_c: .asciz "Ingrese c: "
    msg_d: .asciz "Ingrese d: "
    resultado: .asciz "f = "

.text
.globl main
main:
    # Pedimos el valor de a
    li a7, 4
    la a0, msg_a
    ecall

    li a7, 5
    ecall
    mv s0, a0       # Guardamos a

    # Pedimos el valor de b
    li a7, 4
    la a0, msg_b
    ecall

    li a7, 5
    ecall
    mv s1, a0       # Guardamos b

    # Pedimos el valor de c
    li a7, 4
    la a0, msg_c
    ecall

    li a7, 5
    ecall
    mv s2, a0       # Guardamos c

    # Pedimos el valor de d
    li a7, 4
    la a0, msg_d
    ecall

    li a7, 5
    ecall
    mv s3, a0       # Guardamos d

    # Primer parentesis (5a + 2b + c)
    li t0, 5
    mul t0, t0, s0     # 5a

    li t1, 2
    mul t1, t1, s1     # 2b

    add t0, t0, t1     # 5a + 2b
    add t0, t0, s2     # 5a + 2b + c

    # Segundo parentesis (4d - 3)
    li t1, 4
    mul t1, t1, s3     # 4d
    addi t1, t1, -3    # 4d - 3

    # Resta final sin simplificar la expresion
    sub s4, t0, t1     # f = primer - segundo parentesis

    # Imprimir el mensaje
    li a7, 4
    la a0, resultado
    ecall

    # Imprimir el resultado
    li a7, 1
    mv a0, s4
    ecall

    # Finalizar programa
    li a7, 10
    ecall
```

---

## C · Explicación del procedimiento

Primero declaré los mensajes que se mostrarían en pantalla para solicitar los valores de a, b, c y d. Utilicé `ecall 4` para mostrar cada mensaje y `ecall 5` para leer los números ingresados después guardé los valores en los registros s0, `s1`, `s2` y `s3`.

Luego resolví la expresión por partes para respetar los paréntesis. Comencé calculando `5a + 2b + c`, utilizando `mul` para las multiplicaciones y `add` para las sumas, el resultado de esta primera parte quedó guardado en `t0`.

Después calculé `4d - 3`, multiplicando el valor de d por 4 y restándole 3 con `addi` este segundo resultado quedó guardado en `t1`.

Finalmente, resté ambos resultados utilizando `sub` y guardé el valor de `f` en el registro `s4`. Para mostrarlo en consola, utilicé `ecall 4` para imprimir el mensaje y `ecall 1` para mostrar el resultado numérico.

---

## D · Resultado esperado

Para comprobar el funcionamiento del programa se pueden ingresar los siguientes valores:

**a = 2, b = 3, c = 4, d = 5**

```text
Ingrese a: 2
Ingrese b: 3
Ingrese c: 4
Ingrese d: 5
f = 3
```

**Comprobación matemática:**

`f = (5(2) + 2(3) + 4) - (4(5) - 3)`

`f = (10 + 6 + 4) - (20 - 3)`

`f = 20 - 17`

**Resultado final: `f = 3`**

Este es el resultado esperado para los valores de prueba, el programa también permite ingresar otros números y calcular el valor correspondiente de `f`.
