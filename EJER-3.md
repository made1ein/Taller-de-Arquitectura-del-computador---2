# Ejercicio 3: Operaciones con registros

**Responsable:** Madelein · **Revisor (PR):**Alejandra

---

## A · Enunciado

Calcular la siguiente expresión utilizando los valores definidos en el ejercicio:

`g = (17a + b + 5c) - [(a - d) + (3e + 3f) + 30]`

**Valores:** a = 4, b = 7, c = 2, d = 3, e = 5, f = 1.

Se deben cargar los valores utilizando `li`, respetar los paréntesis sin simplificar la expresión y mostrar el resultado en consola

---

## B · Código desarrollado

**Archivo:** `ej03.asm`

```asm
.data
    mensaje: .asciz "g = "

.text
.globl main
main:
    # Guardamos los valores
    li s0, 4
    li s1, 7
    li s2, 2
    li s3, 3
    li s4, 5
    li s5, 1

    # Primer parentesis
    li t0, 17
    mul t0, t0, s0
    add t0, t0, s1

    li t1, 5
    mul t1, t1, s2
    add t0, t0, t1

    # Segundo parentesis y corchete
    sub t1, s0, s3

    li t2, 3
    mul t2, t2, s4

    li t3, 3
    mul t3, t3, s5

    add t2, t2, t3
    add t1, t1, t2
    addi t1, t1, 30

    # Resultado final
    sub s6, t0, t1

    # Imprimir resultado
    li a7, 4
    la a0, mensaje
    ecall

    li a7, 1
    mv a0, s6
    ecall

    li a7, 10
    ecall
```

---

## C · Explicación del procedimiento

Primero guardé los valores de las variables en los registros `s0` hasta `s5` utilizando `li`, ya que estaban definidos en el enunciado

Después resolví la expresión por partes para respetar los paréntesis, comencé calculando `17a + b + 5c`, obteniendo 85 ,luego resolví el contenido del corchete calculando `a - d` y `3e + 3f` para finalmente sumar 30 y obtener 49

Una vez que tenía ambos resultados realicé la resta `85 - 49` utilizando `sub` y guardé el valor final en `s6`por último, utilicé `ecall 4` y `ecall 1` para mostrar el resultado en consola

---

## D · Resultado esperado

```text
g = 36
```

**Comprobación:** El resultado matemático es 36. La ejecución en RARS debe confirmar esta salida

---

