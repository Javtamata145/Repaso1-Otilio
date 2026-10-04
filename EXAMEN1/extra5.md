# Ejercicios Día 5: Intel x86

**Temas:** segmentación y modo real del 8086, buses de la familia Intel, sintaxis AT&T de Pentium, prólogo de funciones, retorno lejano, CISC vs RISC y niveles de privilegio.
**Tiempo sugerido:** 60 a 90 minutos.

**Recuerda:** en modo real, dirección física = segmento × 16 + desplazamiento (se agrega un 0 hexadecimal al segmento y se suma el desplazamiento).

---

## Ejercicios

**1.** El 8086 está en modo real con DS = 0x1A00 y SI = 0x0250, y ejecuta `MOV AX, DS:[SI]`. Escribe la dirección física, la efectiva y la lógica.

**2.** DS = 0x0F00 y BX = 0x0A5C con `MOV AX, DS:[BX]`. ¿Cuál es la dirección física?

**3.** Una dirección física es 0x23456 y el segmento es 0x2000. ¿Cuál es el desplazamiento?

**4.** Con CS = 0xFFFF e IP = 0x000F, ¿cuál es la dirección física de la instrucción?

**5.** Completa la tabla de buses y capacidad máxima de memoria:

| Procesador | Bus de datos | Bus de direcciones | Capacidad |
|---|---|---|---|
| 8086 | | | |
| 80286 | | | |
| 80386 | | | |

**6.** ¿En cuántas partes dividen o segmentan la memoria los microprocesadores Intel y cuáles son? ¿Cuál segmento se usa para la pila?

**7.** Explica qué hace cada instrucción en sintaxis AT&T (x86-64):
- a) `movl $5, -4(%rbp)`
- b) `movl -4(%rbp), %eax`
- c) `addl %edx, %eax`
- d) `leaq -20(%rbp), %rsi`
- e) `pushq %rbp`
- f) `movq %rsp, %rbp`
- g) `popq %rbp`
- h) `ret`

**8.** Si RBP = 0x7FFF0010, ¿qué valor queda en RSI después de `leaq -20(%rbp), %rsi`? ¿Cuál es la diferencia con `movl -20(%rbp), %esi`?

**9.** Una función x86-64 empieza con:
```asm
pushq %rbp
movq  %rsp, %rbp
subq  $16, %rsp
```
Si RSP valía 0x7FFF0100 justo antes de la instrucción `call` que la llamó, calcula el valor de RSP después del `call`, después de `pushq %rbp`, después de `subq` y la dirección que referencia `-4(%rbp)`.

**10.** En un 8086, SP = 0xFFF0 y se ejecuta un `RET` lejano. ¿Qué valores se sacan de la pila, en qué orden y cuánto vale SP al terminar? ¿En qué se diferencia de un `RET` cercano?

**11.** ¿Cuántos niveles de privilegio tienen Intel y ARM? ¿Cuántos bits se necesitan para codificar los de Intel y qué nivel usa el sistema operativo?

**12.** Menciona tres diferencias entre las arquitecturas Pentium y ARM.

**13.** ¿Qué registros utiliza el Pentium para manejar la pila? ¿Cómo se llaman en 64 bits?

**14.** Un procesador Intel en modo real ejecuta `call L3`:
- a) Si el PC antes de ejecutar la instrucción es 0x4A10 y la instrucción mide 3 bytes, ¿qué valor del PC se guarda en la pila?
- b) Si fuera una llamada lejana de 5 bytes con CS:IP = 0x1000:0x2200, ¿qué valores se guardan?

**15.** El 80286 se usaba en la PC AT. ¿De cuántos bits es su bus de datos y de cuántos su bus de direcciones? ¿Qué capacidad direcciona?

---

## Respuestas

**1.** Física = 0x1A00 × 16 + 0x0250 = 0x1A000 + 0x0250 = **0x1A250**. Efectiva = **0x0250**. Lógica = **0x1A00:0x0250**.

**2.** 0x0F000 + 0x0A5C = **0x0FA5C**.

**3.** 0x23456 − 0x20000 = **0x3456**.

**4.** 0xFFFF0 + 0x000F = **0xFFFFF** (la última dirección del 1 MB).

**5.**

| Procesador | Bus de datos | Bus de direcciones | Capacidad |
|---|---|---|---|
| 8086 | 16 bits | 20 bits | 1 MB |
| 80286 | 16 bits | 24 bits | 16 MB |
| 80386 | 32 bits | 32 bits | 4 GB |

**6.** Hasta **6 segmentos**: código (CS), datos (DS), pila (SS) y datos extra (ES, FS, GS); en el 8086 original eran 4 (CS, DS, SS, ES). La pila usa **SS**.

**7.**
- a) Guarda el valor 5 (32 bits) en la memoria en la dirección RBP − 4.
- b) Copia a EAX el valor de 32 bits que está en RBP − 4.
- c) EAX ← EAX + EDX (32 bits).
- d) Calcula RBP − 20 y deja esa dirección en RSI (no lee memoria).
- e) Resta 8 a RSP y guarda ahí el valor de RBP (64 bits).
- f) Copia RSP a RBP (RBP queda como puntero base del marco).
- g) Saca de la pila 64 bits hacia RBP y suma 8 a RSP.
- h) Saca de la pila la dirección de retorno y la pone en RIP.

**8.** RSI = 0x7FFF0010 − 0x14 = **0x7FFEFFFC**. `leaq` solo calcula la dirección; `movl -20(%rbp), %esi` va a memoria y trae el **contenido** de 32 bits que hay en esa dirección.

**9.**
- Después del `call` (guarda la dirección de retorno de 8 bytes): RSP = 0x7FFF0100 − 8 = **0x7FFF00F8**.
- Después de `pushq %rbp`: RSP = **0x7FFF00F0**; con `movq %rsp,%rbp`, RBP = 0x7FFF00F0.
- Después de `subq $16, %rsp`: RSP = **0x7FFF00E0**.
- `-4(%rbp)` = 0x7FFF00F0 − 4 = **0x7FFF00EC**.

**10.** Un `RET` lejano saca primero el **IP** (en [SP], 0xFFF0) y después el **CS** (en [SP+2]); SP termina en 0xFFF0 + 4 = **0xFFF4**. Un `RET` cercano solo saca el IP (SP aumenta 2).

**11.** Intel tiene **4** niveles (anillos 0, 1, 2, 3; códigos 00, 01, 10, 11) y necesita **2 bits**; el sistema operativo es el único en el nivel **0**. ARM tiene **2** niveles (0, 1), o sea 1 bit.

**12.** Tres posibles: (1) Pentium es CISC y ARM es RISC; (2) Pentium tiene instrucciones de longitud variable, ARM las tiene de longitud fija (32 bits, o 16/32 en Thumb-2); (3) Pentium puede operar directamente con memoria, ARM es de carga/almacenamiento (solo `LDR`/`STR` acceden a memoria). También: número de registros, niveles de privilegio (4 vs 2).

**13.** **ESP** (puntero de pila) y **EBP** (puntero base del marco). En 64 bits: **RSP** y **RBP**.

**14.**
- a) Se guarda el PC de la instrucción siguiente: 0x4A10 + 3 = **0x4A13**.
- b) Se guarda primero **CS = 0x1000** y luego **IP = 0x2200 + 5 = 0x2205**.

**15.** Bus de datos de **16 bits**, bus de direcciones de **24 bits**, capacidad de 2^24 = **16 MB**.