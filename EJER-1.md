# Ejercicio 1: Leer un número y mostrarlo

**Responsable:** D’alessandro · **Revisor (PR):** Madelein

---

## A · Enunciado

Desarrollar un programa que solicite un número al usuario con el mensaje `Ingrese numero: ` y después muestre el mismo valor acompañado del mensaje `El numero es: `.

Se debe utilizar `.data` para declarar los mensajes, emplear registros con notación ABI y finalizar el programa utilizando `ecall`.

---

## B · Código desarrollado

**Archivo:** `ej01.asm`

```asm
.data
    msg_in:  .asciz "Ingrese numero: "
    msg_out: .asciz "El numero es: "

.text
.globl main
main:
    # Pedimos el numero
    li a7, 4
    la a0, msg_in
    ecall

    # Leemos el numero
    li a7, 5
    ecall
    mv s0, a0

    # Mostramos el mensaje de salida
    li a7, 4
    la a0, msg_out
    ecall

    # Imprimimos el numero ingresado
    li a7, 1
    mv a0, s0
    ecall

    # Finalizamos el programa
    li a7, 10
    ecall
```

---

## C · Explicación del procedimiento

Primero declaré los dos mensajes en la sección `.data` utilizando `.asciz`, que permite guardar las cadenas de texto. Después mostré el mensaje `Ingrese numero: ` con `ecall 4`, colocando la dirección del texto en el registro `a0`.

Luego utilicé `ecall 5` para leer el número ingresado y lo guardé en `s0` mediante `mv`. Esto permite conservar el valor, ya que el registro `a0` también se utiliza para imprimir los mensajes.

Una vez guardado el número, mostré el mensaje `El numero es: ` utilizando nuevamente `ecall 4`. Después copié el valor de `s0` a `a0` para imprimirlo con `ecall 1`.

Finalmente, utilicé `ecall 10` para terminar la ejecución del programa.

---

## D · Resultado esperado

Para comprobar el funcionamiento del programa, ingresamos el número 7.

```text
Ingrese numero: 7
El numero es: 7
```

**Comprobación:** El programa debe mostrar el mismo número que ingresó el usuario. En este ejemplo se utiliza el valor 7, pero también puede funcionar con otros números enteros.
