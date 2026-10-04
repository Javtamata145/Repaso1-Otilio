# Ejercicios Día 1: Fundamentos

**Temas:** conceptos básicos, Von Neumann y Harvard, tipos de arquitectura (pila, acumulador, registros), PC y saltos, tiempo de ejecución.
**Tiempo sugerido:** 60 a 90 minutos. Resuelve sin mirar la guía y revisa al final. Los ejercicios son del mismo estilo que los de tus exámenes pero con datos distintos.

---

## Ejercicios

**1.** Un programa tiene 25,000 instrucciones. La arquitectura tarda 6 ciclos de reloj por instrucción y tiene un cristal de 12 MHz. ¿Cuánto tiempo tarda en ejecutarse?

**2.** Un programa de 8,000 instrucciones se ejecuta en una arquitectura que tarda 3 ciclos por instrucción con un cristal de 24 MHz. ¿Cuánto tiempo tarda?

**3.** Una arquitectura con cristal de 100 MHz tarda 5 ciclos por instrucción. Si el programa debe terminar en 50 µs, ¿cuántas instrucciones puede tener como máximo?

**4.** Un programa de 60,000 instrucciones, de 2 ciclos cada una, debe terminar en 10 ms. ¿Cuál es la frecuencia mínima del cristal?

**5.** Define *arquitectura de computadoras* y menciona cinco características que debes conocer para describir la arquitectura de un sistema.

**6.** Clasifica cada uno como **microprocesador** o **microcontrolador**: Pentium, ATmega328P, 80286, PIC18F4550, TM4C1294NCPDT, STM32F103C8. Después explica la diferencia en una frase.

**7.** Explica la diferencia entre arquitectura Von Neumann y Harvard (mínimo dos diferencias). Clasifica ATmega328P, PIC18F4550 e Intel 8086. ¿Por qué una arquitectura Harvard puede tener instrucciones de 16 bits y datos de 8 bits?

**8.** Escribe en una tabla la secuencia para `D = A + B − C` en una arquitectura de **pila**, de **acumulador** y de **registros de propósito general** (tipo load/store).

**9.** Saltos y PC:
- a) ¿Cuántos tipos de saltos existen respecto al PC y cuáles son?
- b) Una instrucción de salto relativo de 2 bytes está en la dirección 0x1000 y su desplazamiento es +0x10, medido desde la instrucción siguiente. ¿A qué dirección salta?
- c) Una instrucción de salto relativo de 2 bytes está en 0x2000 y su desplazamiento es −0x08, medido desde la instrucción siguiente. ¿A qué dirección salta?

**10.** Incremento del PC:
- a) En un PIC18F4550 el PC vale 0x0100. Se ejecutan en orden una instrucción de 16 bits, una de 32 bits y otra de 16 bits. ¿Qué valores toma el PC después de cada una?
- b) En un ATmega328P el PC (en palabras) vale 0x0100. Se ejecutan en orden una instrucción de 16 bits, una de 32 bits y otra de 16 bits. ¿Qué valores toma el PC después de cada una?

**11.** Dibuja una computadora virtual con CPU de registros de 8 bits, ROM de 8 KB y RAM de 8 KB (ambas organizadas en bytes) y un puerto de E/S. Indica los anchos del bus de datos y del bus de direcciones, el tamaño mínimo del PC y del SP, y cómo se separan ROM y RAM en el mapa de memoria.

**12.** Un procesador direcciona palabras de 32 bits con 16 líneas de dirección. ¿Cuál es su resolución y cuál su capacidad en KB?

---

## Respuestas

**1.** 25,000 × 6 = 150,000 ciclos. 150,000 / 12 MHz = **12.5 ms**.

**2.** 8,000 × 3 = 24,000 ciclos. 24,000 / 24 MHz = **1 ms**.

**3.** Ciclos disponibles = 50 µs × 100 MHz = 5,000 ciclos. 5,000 / 5 = **1,000 instrucciones**.

**4.** Ciclos = 60,000 × 2 = 120,000. Frecuencia = 120,000 / 0.010 s = **12 MHz**.

**5.** Es el conjunto de atributos del sistema visibles para el programador (no cómo está construido por dentro). Cinco de estas: ancho de palabra y de buses, conjunto y formato de instrucciones, registros (PC, SP, banderas), modos de direccionamiento, organización de memoria (Von Neumann o Harvard, endianness, alineación), manejo de pila, interrupciones, E/S y niveles de privilegio.

**6.** Microprocesadores: **Pentium** y **80286**. Microcontroladores: **ATmega328P, PIC18F4550, TM4C1294NCPDT, STM32F103C8**. El microprocesador es solo la CPU y necesita memoria y periféricos externos; el microcontrolador integra CPU, memoria y periféricos en un solo chip.

**7.** Von Neumann: una sola memoria y un solo bus para instrucciones y datos; Harvard: memorias y buses separados. En Von Neumann instrucción y dato no pueden leerse a la vez (cuello de botella); en Harvard sí. Clasificación: **ATmega328P y PIC18F4550 son Harvard**; **8086 es Von Neumann**. Como las memorias son independientes, cada una puede tener su propio ancho de palabra.

**8.** `D = A + B − C`:

| Pila | Acumulador | Registros (load/store) |
|---|---|---|
| `PUSH A` | `LOAD A` | `LOAD R1, A` |
| `PUSH B` | `ADD B` | `LOAD R2, B` |
| `ADD` | `SUB C` | `LOAD R3, C` |
| `PUSH C` | `STORE D` | `ADD R4, R1, R2` |
| `SUB` | | `SUB R4, R4, R3` |
| `POP D` | | `STORE D, R4` |

**9.**
- a) **Dos**: absoluto (el PC se carga con una dirección específica) y relativo (se le suma una constante al PC). Cada uno puede ser condicional o incondicional.
- b) PC después del fetch = 0x1002; 0x1002 + 0x10 = **0x1012**.
- c) PC después del fetch = 0x2002; 0x2002 − 0x08 = **0x1FFA**.

**10.**
- a) PIC18F4550 (bytes): 0x0100 → **0x0102** → **0x0106** → **0x0108**.
- b) ATmega328P (palabras): 0x0100 → **0x0101** → **0x0103** → **0x0104**.

**11.** Memoria total = 8 KB + 8 KB = 16 KB = 2^14 bytes.
- **Bus de datos:** 8 líneas. **Bus de direcciones:** 14 líneas.
- **PC y SP:** al menos 14 bits.
- **Mapa:** ROM en 0x0000 a 0x1FFF (A13 = 0) y RAM en 0x2000 a 0x3FFF (A13 = 1). El diagrama debe incluir CPU (ALU, registros, PC, IR, SP, banderas), ROM, RAM, puerto y los tres buses.

**12.** Resolución = **32 bits** (4 bytes, es la unidad mínima direccionable). Capacidad = 2^16 palabras × 4 bytes = 262,144 bytes = **256 KB**.