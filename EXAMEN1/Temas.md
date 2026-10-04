# Arquitectura de Computadoras: preguntas transcritas

**Universidad Autónoma de Yucatán, Facultad de Matemáticas**

Transcribí las 18 imágenes de la carpeta *Examenes*. Resultaron ser **9 exámenes distintos** con **95 preguntas** en total, porque algunas imágenes son el mismo examen:

| Examen | Imágenes que lo contienen | Preguntas |
|---|---|---|
| A | Examen1 | 10 |
| B | Examen2 y Examen16 (es la misma hoja, calificada) | 10 |
| C | Examen3 a Examen11 (capturas de pantalla del archivo del profesor *Examen_Arq_segundo_2024* con la clave de respuestas, y dos fotos de una hoja resuelta) | 10 |
| D | Examen12 | 10 |
| E | Examen13 | 10 |
| F | Examen14 | 10 |
| G | Examen15 | 15 |
| H | Examen17 | 10 |
| I | Examen18 | 10 |

Cada pregunta tiene un código (por ejemplo **C7** es la pregunta 7 del examen C). Ese mismo código se usa en la guía de repaso y en su tabla de temas.

Convenciones: dejé la redacción tal como aparece, incluyendo erratas del original (por ejemplo "Hardvad"). Lo que está entre corchetes son aclaraciones mías. Omití los nombres de los alumnos.

---

## Examen A (imagen Examen1)

*INSTRUCCIONES: Lee cuidadosamente cada inciso y responde lo que se pregunta.*

**A1.** En los programas normalmente se ejecuta una instrucción y luego la siguiente, en ocasiones hay que hacer saltos condicionales o incondicionales. ¿Respecto al PC cuántos y cuáles saltos existen?

**A2.** ¿Cuál es la función principal de la memoria llamada Stack?

**A3.** Un programa tiene 10,000 instrucciones. Este programa se ejecuta en una arquitectura que tarda 4 ciclos de reloj por cada instrucción, si la arquitectura tiene un cristal de 200MHz, ¿Cuánto tiempo tarda el programa en ejecutarse?

**A4.** Para los microcontroladores Atmega328p, PIC18F4550 y TM4C1294NCPDT, haga los algoritmos a detalle, para escribir 100 localidades de memoria con el valor 0x00 iniciando en la dirección más baja de la memoria RAM disponible para el programador.

**A5.** Supongamos que se requiere desplegar en el monitor una resolución de 1024X768, a 32 colores, ¿Cuánta Memoria se necesita?

**A6.** Si la última operación ejecutada en una computadora con palabra de 8 bits fue una suma en la que los dos operandos eran -129 y -3, ¿Cuál sería el valor de los siguientes indicadores?
- Acarreo
- Cero
- Desbordamiento (overflow)
- Signo
- Acarreo intermedio

**A7.** ¿Qué se entiende por arquitectura acumulador en los microprocesadores?

**A8.** Un microprocesador tiene 20 líneas en el bus de direcciones, 8 líneas en el bus de datos y todos sus registros internos son de 8 bits. ¿Cuál es el menor entero con signo que se puede representar en esta arquitectura?

**A9.** Cuando se dice que un microprocesador es de 16 bits, ¿Qué significa?

**A10.** En el registro W del PIC18F4550 se tiene cierto valor y se desea escribirlo en la dirección de la memoria RAM cuya dirección es 0XABC. Escriba las instrucciones necesarias para hacerlo, use direccionamiento directo e indirecto.

---

## Examen B (imágenes Examen2 y Examen16)

*Prueba de desempeño de Arquitectura de Computadora. Las preguntas B1 a B4 comparten este enunciado:*
*Un microprocesador tiene 16 líneas en el bus de datos, 24 líneas en el bus de direcciones y sus instrucciones tienen una longitud de 16 y 32 bits, si es arquitectura Von Neumann y su memoria está organizada en palabras de 16 bits.*

**B1.** ¿De qué tamaño máximo puede ser la memoria en byte?

**B2.** ¿De cuántos bits, cuando menos, debe ser el puntero de pila?

**B3.** ¿Cuántas instrucciones se pueden colocar en su memoria?

**B4.** Elabore un apuntador para mover los 8 últimos bits que se encuentran en la memoria.

**B5.** Un microprocesador tiene un ancho de bus de datos de 32 bits y puede mover datos tamaño byte, word y doble word, es decir de 8, 16 y 32 bits; su bus de direcciones es de 32 bits. En este procesador se llama la siguiente función: `sum(a,b,c,d)`. Si los parámetros a, b, c y d son enteros de 32 bits, dé un esquema de ¿cómo queda la pila después de llamar la función suma? Asuma que la cima de la pila es la dirección 00001000H. (10 puntos)

**B6.** En un mismo procesador pueden diferenciarse hasta 3 espacios de direcciones de memoria diferentes, ¿Cuáles son?

**B7.** Mencione los pasos que ejecuta una computadora cuando se prende.

**B8.** ¿Cuándo se dice que un conjunto de instrucciones es ortogonal?

**B9.** ¿Qué se entiende por valor inmediato?

**B10.** ¿Qué se entiende por computadoras que son arquitecturas de 16 o 32 bits?

---

## Examen C (imágenes Examen3 a Examen11)

*Prueba de desempeño de Arquitectura de Computadora. Cada pregunta vale 10 puntos.*

**C1.** El registro DS tiene el valor 0x0020 y BX tiene el valor 0x00FF, si el 8086 está trabajando en modo real y se tiene la instrucción `MOV AX, DS:[BX]`. Escriba lo siguiente: (10 puntos)
- a) La dirección física
- b) La dirección efectiva
- c) La dirección lógica

**C2.** Qué se entiende por arquitectura de pila. (10 puntos)

**C3.** Explique los dos tipos de direccionamiento de datos que tienen los microprocesadores PIC18F4550. (10 puntos)

**C4.** Cuántos niveles de privilegio tienen los microprocesadores ARM e INTEL. (10 puntos)

**C5.** Mencione qué ocurre cuando una computadora se prende. (10 puntos)

**C6.** La dirección base o de datos del puerto C del TM4C1294NCPDT [escrito "M4C1294NCPDT" en el examen] es 0x4005A000, elabore un vector para escribir o leer los bit 3 y 7. (10 puntos)

**C7.** ¿Diferencias entre una interrupción y una llamada a subrutina?, mencione tres. (10 puntos)

**C8.** Explique lo que sucede cuando ocurre una interrupción en el TM4C1294NCPDT. (10 puntos)

**C9.** Explique si las siguientes instrucciones son correctas o no y diga la razón. (10 puntos)
- `MOVLW 0x200` (Pic)
- `MOV R0, #0x20000000` (ARM)
- `MOV AX, EBX` (INTEL)

**C10.** ¿Para qué sirve el registro PC en los microprocesadores? (10 puntos)

---

## Examen D (imagen Examen12)

**D1.** La arquitectura de Von Neumann es del tipo SISD (simple instrucción, simple dato), este tipo de arquitectura necesariamente tiene un registro único ¿llamado?

**D2.** Escriba una ventaja y una desventaja de la Arquitectura Carga / Almacenamiento.

**D3.** Un procesador Intel está funcionando en modo real y ejecuta la siguiente instrucción `call L3`, si el contador de programa antes de ejecutar esta instrucción tiene el valor de 338CH y la instrucción en código máquina es E9533B. ¿Qué valor del PC se guarda en la pila?

**D4.** Escriba una instrucción en código máquina de un microprocesador virtual, explique los campos de que consta la instrucción además el tipo de arquitectura para la cual se diseñó la instrucción.

**D5.** Se sabe que la memoria de programa del PIC18F4550 está organizada en byte y que las instrucciones en código máquina se generan en 16 o 32 bit. ¿Qué implicación tiene esta arquitectura de memoria respecto al PC?

**D6.** ¿Cuál es la diferencia entre las instrucciones `LDI R16, 0x100` y `LDS R16, 0x100` en los microprocesadores Atmega 328P?

**D7.** Explique a detalle el significado de la siguiente instrucción en microprocesadores Intel.
- a) `movl -8(%rbp), %esi`
- b) `leaq -20(%rbp), %rsi`

**D8.** Explique a detalle qué ocurre cuando se llama a una subrutina.

**D9.** Si comparo dos números, ¿Qué tipo de cuidados debo tener?

**D10.** Dibuje una computadora virtual con todos los elementos que la integren (a detalle).

---

## Examen E (imagen Examen13)

*INSTRUCCIONES: Lee cuidadosamente cada inciso y responde lo que se pregunta (10 c/u).*

**E1.** Cuando ocurre una interrupción de prioridad baja en un Pic18F4550, ¿Con qué valor se carga el PC?

**E2.** Explique la razón del ¿Por qué no existe el direccionamiento directo en los microcontroladores ARM?

**E3.** Escriba la instrucción en ensamblador para el atmega328p, el pic18f4550 y el TM4C1294NCPTD para mover el valor 0x4590 a un registro interno del microprocesador.

**E4.** Se sabe que el Atmega328P tiene un PC de 14 bits, ¿Cómo está organizada la memoria de programa?

**E5.** ¿Con qué valores se inicia la pila del Atmega328P, PIC18F4550 y el TM4C1294NCPTD?

**E6.** ¿Qué es Arquitectura de Computadoras?

**E7.** ¿Qué significa arquitectura Von Neumann?

**E8.** ¿Qué significa Arquitectura Hardvad? [Harvard]

**E9.** En el microprocesador Atmega328P, ¿en qué dirección de la memoria RAM se encuentra mapeado el registro interno R10? [el borde derecho de la foto está cortado; la parte final dice "...mapead[o]... registro interno R10"]

**E10.** ¿Qué es ortogonalidad?

---

## Examen F (imagen Examen14)

*INSTRUCCIONES: Lee cuidadosamente cada inciso y responde lo que se pregunta (10 p/u).*

**F1.** Escriba una instrucción en código máquina de un microprocesador virtual, y explique los campos de que consta la instrucción, además, el tipo de arquitectura para la cual se diseñó la instrucción.

**F2.** En las arquitecturas de pila, acumulador y de registros de propósitos generales ¿Dónde se encuentran los operandos de cada arquitectura?

**F3.** Respecto al PC, ¿Cuántos tipos de saltos existen?

**F4.** Explique cómo se inicializa el puntero de pila en el Atmega328P y el STM32F103C8.

**F5.** ¿Por qué no se alinean los datos en el Atmega328P y el STM32F103C8 si? [la pregunta se lee así en la foto; el final parece incompleto]

**F6.** Diga la diferencia entre una llamada a subrutina del Atmega328P y el STM32F103C8.

**F7.** ¿Qué diferencia existe entre el inicio del Atmega328P y el STM32F103C8?

**F8.** ¿Qué es la resolución de un microprocesador?

**F9.** Muestre en una tabla cómo sería la secuencia de código C=A+B para las arquitecturas de pila, de acumulador y de registro de propósitos generales.

**F10.** Explique si existe direccionamiento inmediato y directo en el STM32F103C8, de razonamiento.

---

## Examen G (imagen Examen15)

*Las preguntas del 1 al 6 son del tercer parcial y las preguntas del 1 al 15 es el examen total.*

**G1.** ¿De cuántos bits es el puntero de pila en el Atmega328P, PIC18F4550 Y el STM32F103C8?

**G2.** ¿En cuánto se incrementa el PC del Atmega328P y el PIC18F4550 cuando se ejecuta una instrucción?

**G3.** Explique ¿por qué es necesario dividir la memoria del PIC18F4550 en bancos?

**G4.** ¿Cuál es la dirección donde inicia el vector de interrupciones del Atmega328P, PIC18F4550 y del STM32F103C8?

**G5.** ¿De cuántos bits es la pila de Atmega328P, Pic18F4550 y del STM32F103C8?

**G6.** Si en el repertorio de instrucciones no existen las instrucciones IN y OUT, ¿Qué significa?

**G7.** Escriba los pasos necesarios para configurar la interrupción INT0 del Atmega328P.

**G8.** ¿Para qué sirve la memoria cache y en qué caso se implementa?

**G9.** De acuerdo a la presentación dada en clase escriba el formato de una instrucción y describa los campos.

**G10.** Escriba las instrucciones necesarias para mover 16 bit a partir de la dirección 0x20000000 al registro R5 del STM32F103C8.

**G11.** ¿Qué utilidad tiene la bandera de overflow?

**G12.** ¿Qué registros utiliza Pentium para manejar la pila?

**G13.** Mencione tres diferencias entre la arquitectura Pentium y ARM.

**G14.** ¿Qué características debes saber para conocer la arquitectura de un sistema?

**G15.** ¿Qué diferencia hay entre un microprocesador y un microcontrolador?

---

## Examen H (imagen Examen17)

**H1.** ¿De cuántos bits es el bus de datos del 80286 de Intel?

**H2.** ¿Cuántas y cuáles son las partes en las que los microprocesadores Intel dividen o segmentan la memoria?

**H3.** ¿Qué significa que los puertos estén mapeados a memoria?

**H4.** ¿Qué significa la directiva ALIGN=2?

**H5.** Escribe de tres maneras diferentes cargar la constante 0x2000000 al registro R1.

**H6.** Dibuja a detalle una computadora con su bus de datos, bus de direcciones, registros internos para hacer operaciones, contador de programa, memoria RAM y puertos, los datos deben ser consistentes.

**H7.** Un microprocesador tiene 16 líneas en el bus de datos, 24 líneas en el bus de direcciones y sus instrucciones tienen una longitud de 16 y 32 bits, si es arquitectura Von Neumann y su memoria está organizada en palabras de 8 bits, tiene 16 registros de 32 bits. ¿Cuál es la dirección mínima y máxima de esta arquitectura?

**H8.** ¿Qué hace la instrucción siguiente, en los microprocesadores ARM? `MOVT R3, #0xF123`

**H9.** ¿Cuál es la función principal de la memoria llamada Stack?

**H10.** ¿Cuál es la función del registro PC?

---

## Examen I (imagen Examen18)

**I1.** Un programa tiene 10,000 instrucciones, este programa se ejecuta en una arquitectura que tarda 4 ciclos de reloj para ejecutar cada instrucción, si la arquitectura tiene un cristal de 20MHz, ¿Cuánto tiempo tarda el programa en ejecutarse?

**I2.** ¿Con qué valor se carga el contador de programa cuando se inicia el procesador STM32F103C8?

**I3.** Si la última operación ejecutada en una computadora con palabra de 8 bits fue una suma en la que los dos operandos eran -120 y -3, ¿Cuál sería el valor de los siguientes indicadores?
- Acarreo
- Cero
- Negativo
- Desbordamiento (overflow)

**I4.** Si en un microprocesador Intel 8086 se ejecuta la instrucción `ret` y es un retorno lejano, ¿qué ocurre?

**I5.** Explique a detalle ¿Qué ocurre en los microprocesadores Intel Pentium cuando se ejecuta la instrucción `movl %eax, -4(%rbp)`?

**I6.** En una computadora se pueden diferenciar hasta 3 espacios de direcciones de memoria diferentes, ¿Cuáles son?

**I7.** Un microprocesador tiene 16 líneas en el bus de datos, 32 líneas en el bus de direcciones y sus instrucciones tienen una longitud de 16 y 32 bits, si es arquitectura Von Neumann y su memoria está organizada en palabras de 16 bits, tiene 16 registros de 32 bits. Elabore una instrucción usando un apuntador para mover un byte de dato que se encuentre en la última dirección de memoria.

**I8.** ¿Cuántos bits se requieren para direccionar una memoria de 4KB si la memoria está organizada en palabras de 16 bits?

**I9.** ¿Cuál es la función principal de la memoria llamada Stack?

**I10.** Explique a detalle ¿Qué ocurre en los microprocesadores Intel Pentium cuando se ejecuta la instrucción `pushq %rbp`?

---

## Cosas que noté al transcribir

- Varias preguntas **se repiten casi idénticas** entre exámenes: la función del Stack (A2, H9, I9), la función del PC (C10, H10), el tiempo de ejecución de 10,000 instrucciones (A3, I1), las banderas tras una suma de 8 bits (A6, I3), el microprocesador de 16 líneas de datos y 24 de direcciones (B1 a B4, H7, I7) y el microprocesador virtual con formato de instrucción (D4, F1, G9).
- A6 usa **-129**, que no cabe en 8 bits (el rango es de -128 a 127). I3 es casi la misma pregunta con **-120**, probablemente la versión corregida.
- En F5 y E9 el texto está incompleto en la foto, así que conviene revisarlos contra tus apuntes.