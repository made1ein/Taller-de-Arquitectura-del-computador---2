
# Ejercicio 5: Suma de cuatro números

**Responsable:** D'alessandro · **Revisor (PR):** Madelein
---
## A · Enunciado

Desarrollar un programa que lea cuatro números desde el teclado, los sume y muestre el resultado. Cada vez que se pida un número se debe mostrar el mensaje `Ingrese numero: ` y el resultado debe salir con el mensaje `El resultado es: `.

Se debe utilizar `.data` para declarar los mensajes, emplear registros con notación ABI y finalizar el programa utilizando `ecall`.
---

## B · Código desarrollado

**Archivo:** `ej05.asm`

```asm
.data
    msg_in:  .asciz "Ingrese numero: "
    msg_out: .asciz "El resultado es: "

.text
.globl main
main:
    li s0, 0            # s0 = acumulador de la suma
    li s1, 4            # s1 = cantidad de numeros a leer
    li s2, 0            # s2 = contador de numeros leidos

leer:
    beq s2, s1, mostrar # si ya leyo 4 numeros, ir a mostrar

    # Pedimos el numero
    li a7, 4
    la a0, msg_in
    ecall

    # Leemos el numero y lo acumulamos
    li a7, 5
    ecall
    add s0, s0, a0      # s0 = s0 + numero
    addi s2, s2, 1      # contador++
    j leer

mostrar:
    # Mostramos el mensaje del resultado
    li a7, 4
    la a0, msg_out
    ecall

    # Imprimimos la suma total
    li a7, 1
    mv a0, s0
    ecall

    # Finalizamos el programa
    li a7, 10
    ecall
```

---

## C · Explicación del procedimiento

Primero declaré en la sección `.data` los dos mensajes con `.asciz`. Luego inicialicé tres registros: `s0` como acumulador de la suma en 0, `s1` con la cantidad de números a leer (4) y `s2` como contador en 0. 

Después armé un bucle con la etiqueta `leer`. Al inicio comparo con `beq` si el contador `s2` ya llegó a 4; si es así, salto a `mostrar`. Si no, imprimo `Ingrese numero: ` con `ecall 4` y leo el número con `ecall 5`, que lo deja en `a0`.

Cada número que lee lo sumo al acumulador con `add s0, s0, a0`, le sumo 1 al contador con `addi` y regreso con `j leer` para pedir el siguiente.

Cuando se leyeron los cuatro números, en `mostrar` imprimo `El resultado es: ` con `ecall 4`, copio la suma de `s0` a `a0` y la muestro con `ecall 1`. Finalmente, utilicé `ecall 10` para terminar la ejecución del programa.

---

## D · Resultado esperado

Para comprobar el funcionamiento del programa, ingresamos los números 3, 5, 2 y 10.
```text
Ingrese numero: 3
Ingrese numero: 5
Ingrese numero: 2
Ingrese numero: 10
El resultado es: 20
```

**Comprobación:** El programa debe pedir el mensaje cuatro veces y mostrar la suma de los cuatro números ingresados. En este ejemplo 3 + 5 + 2 + 10 = 20, pero también puede funcionar con otros números enteros.
