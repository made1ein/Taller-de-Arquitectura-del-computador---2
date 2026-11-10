Ejercicio 1: Leer un número y mostrarlo
Responsable: D’alessandro · Revisor (PR): Madelein
A · Enunciado
Escriba un programa que pida un número con el mensaje “Ingrese numero: “ y luego lo muestre con el mensaje “El numero es: “. Use .data para los mensajes y termine el programa con ecall.
Se debe usar la notación ABI para los registros y mostrar mensajes claros al pedir los datos.
B · Código desarrollado
Archivo: ej01.asm
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

    li a7, 1
    mv a0, s0
    ecall

    
    li a7, 10
    ecall
C · Explicación del procedimiento
Primero guardé los dos mensajes en .data con .asciz, para que cada cadena termine en cero y ecall 4 sepa dónde acaba. Luego imprimí “Ingrese numero: “ cargando 4 en a7 y la dirección del mensaje en a0 con la.
Después leí el número con (ecall) 5, que lo deja en a0, lo pasé a s0 con (mv) porque si lo dejaba en a0 se me borraba con el siguiente (ecall), que también usa a0 para el mensaje.
Luego imprimí “El numero es: “ con ecall 4, volví a poner el número en a0 desde s0 y lo mostré con ecall 1. Al final cierro el programa con ecall 10.
D · Resultado esperado
Ingrese numero: 7
El numero es: 7
Comprobación: con cualquier número que se ingrese, el programa debe mostrar exactamente el mismo valor después del mensaje “El número es: “, en RARS debe salir esta salida.
