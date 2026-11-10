# Ejercicio 6: Resto de una división

**Responsable:** Madelein · **Revisor (PR):** Luis

---

## A · Enunciado

Desarrollar un programa que solicite dos números enteros A y B, y calcule el resto de dividir A entre B utilizando la instrucción `rem`.

El programa debe comprobar si B es igual a cero. En ese caso, mostrará el mensaje `No se puede dividir entre cero`, ya que la división no es válida.

Si B es diferente de cero, se calculará el resto de la división. Cuando el resto sea igual a cero, se mostrará también el mensaje `A es múltiplo de B`.

---

## B · Código desarrollado

**Archivo:** `ej06.asm`

```asm
.data
    msg_a:       .asciz "Ingrese A: "
    msg_b:       .asciz "Ingrese B: "
    msg_resto:   .asciz "El resto es: "
    msg_error:   .asciz "No se puede dividir entre cero"
    msg_multiplo: .asciz "A es múltiplo de B"

.text
.globl main

main:
    # Pedimos el valor de A
    li a7, 4
    la a0, msg_a
    ecall

    li a7, 5
    ecall
    mv s0, a0       # Guardamos A

    # Pedimos el valor de B
    li a7, 4
    la a0, msg_b
    ecall

    li a7, 5
    ecall
    mv s1, a0       # Guardamos B

    # Verificamos si B es cero
    beqz s1, error

    # Calculamos el resto de A entre B
    rem s2, s0, s1

    # Mostramos el resto
    li a7, 4
    la a0, msg_resto
    ecall

    li a7, 1
    mv a0, s2
    ecall

    # Salto de linea
    li a7, 11
    li a0, 10
    ecall

    # Comprobamos si el resto es cero
    beqz s2, multiplo

    # Si no es multiplo, terminamos
    j finalizar

error:
    # Mostramos el mensaje de error
    li a7, 4
    la a0, msg_error
    ecall
    j finalizar

multiplo:
    # Mostramos el mensaje de multiplo
    li a7, 4
    la a0, msg_multiplo
    ecall

finalizar:
    # Finalizamos el programa
    li a7, 10
    ecall
```

---

## C · Explicación del procedimiento

Primero declaré los mensajes que se mostrarían en pantalla para solicitar los números A y B, utilicé `ecall 4` para imprimir los mensajes y `ecall 5` para leer los valores ingresados, guardándolos en los registros `s0` y `s1`

Después agregué una condición con `beqz` para comprobar si B era igual a cero. Si se cumple, el programa muestra el mensaje de error y termina sin realizar la división

Si B es diferente de cero, utilizo `rem` para calcular el resto de A entre B y guardarlo en `s2`luego muestro el resultado utilizando `ecall 4` para el mensaje y `ecall 1` para imprimir el número

Finalmente, compruebo si el resto es cero, si lo es, significa que A es múltiplo de B, por lo que se muestra el mensaje correspondiente. En caso contrario, el programa termina después de mostrar el resto

---

## D · Resultados esperados

**Caso 1: Cuando A es múltiplo de B**

Ingresamos A = 12 y B = 4.

```text
Ingrese A: 12
Ingrese B: 4
El resto es: 0
A es múltiplo de B
```

**Comprobación:** Como 12 se divide exactamente entre 4, el resto es 0 y se muestra el mensaje de múltiplo

**Caso 2: Cuando A no es múltiplo de B**

Ingresamos A = 13 y B = 4.

```text
Ingrese A: 13
Ingrese B: 4
El resto es: 1
```

**Comprobación:** Al dividir 13 entre 4, sobra 1. Por eso no aparece el mensaje de múltiplo

**Caso 3: Cuando B es cero**

Ingresamos A = 12 y B = 0.

```text
Ingrese A: 12
Ingrese B: 0
No se puede dividir entre cero
```

**Comprobación:** El programa detecta que B es cero y muestra el mensaje de error sin intentar calcular el resto
