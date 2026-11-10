# Taller de Arquitectura del Computador – RISC-V

## Descripción del proyecto

En este repositorio desarrollaremos los 10 ejercicios del taller de ensamblador RISC-V, utilizando el simulador RARS.

El objetivo es poner en práctica lo aprendido sobre el uso de registros, operaciones aritméticas, entrada y salida de datos, condiciones y bucles. Cada ejercicio se desarrollará por separado y contará con comentarios para facilitar la comprensión del código.

---

## A · Indicaciones generales

- El trabajo se realiza en un grupo de 4 integrantes.
- Utilizar el simulador RARS para desarrollar y ejecutar los programas.
- Emplear registros con notación ABI, como `a0`, `t0`, `s1`, evitando nombres como `x5` o `x10`.
- Guardar cada ejercicio en un archivo `.asm` independiente, desde `ej01.asm` hasta `ej10.asm`.
- Comentar las instrucciones importantes para explicar su funcionamiento.
- Mostrar mensajes claros cuando el programa solicite datos al usuario.
- Cada ejercicio tiene un valor de 2 puntos.

---

## B · Referencia de ecall en RARS

| ecall | Función |
|---|---|
| 1 | Imprime un número entero. |
| 4 | Imprime una cadena de texto. |
| 5 | Lee un número entero. |
| 8 | Lee una cadena de texto. |
| 11 | Imprime un carácter. |
| 10 | Finaliza el programa. |

Para utilizar estas operaciones, se coloca el número del servicio en el registro `a7` y se ejecuta `ecall`.

---

## C · Organización de los ejercicios

### Parte A · Conceptos básicos (Ejercicios 1 al 4)

En esta primera parte trabajaremos con instrucciones básicas de RISC-V, como guardar valores en registros, solicitar datos y realizar operaciones aritméticas.

- **Ejercicio 1:** Lectura e impresión de un número.
- **Ejercicio 2:** Ingreso de nombre y edad.
- **Ejercicio 3:** Operaciones aritméticas con valores definidos.
- **Ejercicio 4:** Operaciones con valores ingresados por teclado.

### Parte B · Operaciones y decisiones (Ejercicios 5 y 6)

En esta parte utilizaremos operaciones y condiciones para que el programa pueda realizar diferentes acciones según los valores ingresados.

- **Ejercicio 5:** Suma de cuatro números.
- **Ejercicio 6:** Cálculo del resto de una división y verificación de múltiplos.

### Parte C · Bucles simples (Ejercicios 7 y 8)

Aquí trabajaremos con instrucciones repetitivas que permiten ejecutar operaciones varias veces hasta cumplir una condición.

- **Ejercicio 7:** Generación de una serie numérica.
- **Ejercicio 8:** Suma de números impares hasta ingresar cero.

### Parte D · Bucles dobles (Ejercicios 9 y 10)

En esta última parte utilizaremos bucles anidados para generar figuras y patrones en la consola.

- **Ejercicio 9:** Creación de un rectángulo de asteriscos.
- **Ejercicio 10:** Generación de un patrón de letras.

---

## D · Organización del equipo

| Integrante | Ejercicios asignados |
|---|---|
| Integrante 1 | Pendiente |
| Integrante 2 | Pendiente |
| Integrante 3 | Pendiente |
| Integrante 4 | Pendiente |

Cada integrante será responsable de desarrollar sus ejercicios, comprobar su funcionamiento en RARS y subir los archivos correspondientes al repositorio.

---

## E · Uso de inteligencia artificial (IA)

Durante el desarrollo del taller utilizamos la inteligencia artificial como herramienta de apoyo para organizar y mejorar la presentación del repositorio en GitHub.

También nos ayudó a comprender mejor las instrucciones de RISC-V, orientarnos en el desarrollo de los códigos y reforzar nuestros conocimientos sobre los temas trabajados en clase.
