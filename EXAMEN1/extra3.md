# Ejercicios Día 3: Pila, subrutinas, interrupciones y arranque

**Temas:** el Stack y el SP, marcos de pila, llamadas y retornos (AVR, PIC, ARM, Intel), interrupciones y vectores, configuración de INT0, arranque y reset.
**Tiempo sugerido:** 60 a 90 minutos.

---

## Ejercicios

**1.** Un procesador de 32 bits tiene la cima de la pila en la dirección 00002000H, la pila crece hacia abajo y se llama a `f(a,b,c)` con parámetros enteros de 32 bits, empujados de derecha a izquierda. Dibuja cómo queda la pila después de la llamada e indica dónde queda el SP. ¿Dónde quedaría el EBP guardado si la función hace `push ebp`?

**2.** Procesador de 16 bits (8086), pila que crece hacia abajo, SP = 0100H antes de llamar a `g(a,b,c,d)` con parámetros de 16 bits y una llamada cercana. Dibuja la pila y da el SP final.

**3.** ATmega328P con SP = 0x08FF. Se ejecuta en orden `PUSH R16`, `PUSH R17`, `CALL f` (la dirección de retorno ocupa 2 bytes), y dentro de `f` solo hay un `RET`. Después se ejecutan `POP R17` y `POP R16`. Da el SP después de cada instrucción.

**4.** Un procesador Intel en modo real ejecuta una llamada cercana de 3 bytes en la dirección 1200H. ¿Qué valor se guarda en la pila? Si fuera una llamada lejana de 5 bytes en CS:IP = 2000H:0400H, ¿qué valores se guardan y en qué orden?

**5.** Completa la tabla: ¿dónde se guarda la dirección de retorno al ejecutar una llamada en cada procesador, y cuánto ocupa?

| Procesador | Dónde | Tamaño |
|---|---|---|
| ATmega328P | | |
| PIC18F4550 | | |
| STM32F103C8 (con `BL`) | | |
| Intel 8086 (llamada cercana) | | |
| Pentium de 64 bits | | |

**6.** Ordena los pasos que ocurren cuando sucede una interrupción en el TM4C1294NCPDT: (a) se ejecuta el servicio; (b) se carga el PC con la dirección del vector de interrupciones; (c) se suspende la ejecución del programa en curso; (d) se retorna de la interrupción; (e) se salta a la dirección correspondiente; (f) se borra la bandera de interrupción; (g) se carga el registro LR con la dirección de retorno.

**7.** Menciona tres diferencias entre una interrupción y una llamada a subrutina, y una cosa que tengan en común.

**8.** Completa:
- a) ¿Con qué valor se carga el PC cuando ocurre una interrupción de **prioridad alta** en el PIC18F4550?
- b) ¿Y una de prioridad baja?
- c) ¿En qué dirección está el vector de INT1 del ATmega328P?
- d) En el STM32F103C8, ¿de qué dirección lee el hardware el valor inicial del SP y de cuál el valor inicial del PC?

**9.** Escribe el programa en ensamblador del ATmega328P (con inicialización de la pila) para que se genere una interrupción INT0 por **flanco de subida**. Indica qué hace cada bloque.

**10.** Escribe los cinco pasos que ocurren cuando se prende una computadora. ¿Con qué valores arrancan el SP y el PC en un STM32F103C8?

**11.** El PIC18F4550 tiene una pila de hardware de 31 niveles. ¿Qué pasa si se anidan 32 llamadas sin retornar?

**12.** En un ARM, la subrutina `A` llama a la subrutina `B` con `BL B` y no guarda LR. ¿Qué problema aparece y cómo se corrige?

**13.** Tabla de la pila: ¿cuántos bits tiene el puntero y cuántos cada entrada de la pila en ATmega328P, PIC18F4550 y STM32F103C8? Además, en el STM32 con SP = 0x20005000 se ejecutan tres `PUSH` de un registro de 4 bytes cada uno. ¿Cuánto vale SP al final?

---

## Respuestas

**1.** Se empujan c, b, a y luego la dirección de retorno:

| Dirección | Contenido |
|---|---|
| 00002000H | (cima antes de llamar) |
| 00001FFCH | c |
| 00001FF8H | b |
| 00001FF4H | a |
| 00001FF0H | dirección de retorno ← **SP** |

Con `push ebp`, el EBP guardado queda en **00001FECH**.

**2.** Cada entrada ocupa 2 bytes. Se empujan d, c, b, a y la dirección de retorno (IP):

| Dirección | Contenido |
|---|---|
| 00FEH | d |
| 00FCH | c |
| 00FAH | b |
| 00F8H | a |
| 00F6H | IP de retorno ← **SP final = 00F6H** |

**3.**

| Instrucción | SP después |
|---|---|
| `PUSH R16` | 0x08FE |
| `PUSH R17` | 0x08FD |
| `CALL f` | 0x08FB |
| `RET` | 0x08FD |
| `POP R17` | 0x08FE |
| `POP R16` | 0x08FF |

**4.** Llamada cercana: se guarda el IP de la instrucción siguiente = 1200H + 3 = **1203H**. Llamada lejana: primero se guarda **CS = 2000H** y luego **IP = 0400H + 5 = 0405H**; el SP baja 4 bytes en total.

**5.**

| Procesador | Dónde | Tamaño |
|---|---|---|
| ATmega328P | Pila en la SRAM | 2 bytes |
| PIC18F4550 | Pila de hardware (aparte de la RAM) | 21 bits |
| STM32F103C8 (con `BL`) | Registro **LR** (no usa la pila a menos que la subrutina llame a otra) | 32 bits |
| Intel 8086 (llamada cercana) | Pila | 2 bytes |
| Pentium de 64 bits | Pila | 8 bytes |

**6.** **c → g → b → e → a → f → d**.

**7.** Diferencias: (1) la subrutina la invoca el programador, la interrupción ocurre cuando sucede un evento; (2) en la subrutina el PC se carga con la dirección de la subrutina, en la interrupción con la dirección del vector de interrupciones; (3) la subrutina se termina con una instrucción de retorno, la interrupción con retorno de interrupción. En común: ambas guardan la dirección de retorno y después la recuperan para continuar el programa.

**8.**
- a) **0x0008**.
- b) **0x0018**.
- c) **0x0004** (el Reset es 0x0000, INT0 0x0002, INT1 0x0004).
- d) El SP se lee de **0x00000000** y el PC (Reset handler) de **0x00000004**.

**9.**
```asm
.org 0x0000
    rjmp RESET              ; vector de Reset
.org 0x0002
    rjmp INT0_ISR           ; vector de INT0

RESET:
    ldi  r16, high(RAMEND)  ; inicializa la pila
    out  SPH, r16
    ldi  r16, low(RAMEND)
    out  SPL, r16

    cbi  DDRD, 2            ; PD2 (INT0) como entrada
    ldi  r16, (1<<ISC01)|(1<<ISC00)   ; ISC01:ISC00 = 11 → flanco de subida
    sts  EICRA, r16         ; EICRA está en I/O extendido
    ldi  r16, (1<<INT0)
    out  EIMSK, r16         ; habilita INT0
    sei                     ; habilita interrupciones globales

main: rjmp main             ; programa principal

INT0_ISR:
    ; ... servicio de la interrupción ...
    reti                    ; retorno de interrupción
```

**10.** (1) El PC se carga con una dirección de memoria (la del reset); (2) se lee la instrucción de esa dirección; (3) se ejecuta; (4) se incrementa el PC y apunta a la siguiente instrucción; (5) se repite desde el paso 2. En el STM32F103C8: el **SP** se carga con la palabra de la dirección **0x00000000** y el **PC** con la palabra de la dirección **0x00000004** (Reset handler).

**11.** La pila de hardware se desborda: se activa el bit de desbordamiento (STKFUL) y, según la configuración del dispositivo, puede provocar un reset. La pila de 31 niveles no se puede ampliar.

**12.** `BL B` sobrescribe LR con la dirección de retorno a `A`; si `A` no la guardó, al terminar `A` ya no sabe a dónde volver. Se corrige guardando LR al inicio de `A` con `PUSH {LR}` y recuperándolo al final con `POP {PC}`.

**13.**

| | Puntero | Entrada de la pila |
|---|---|---|
| ATmega328P | 12 bits efectivos (SPH:SPL) | 8 bits |
| PIC18F4550 | 5 bits (STKPTR) | 21 bits |
| STM32F103C8 | 32 bits | 32 bits |

Tres `PUSH` de 4 bytes = 12 bytes = 0xC. SP final = 0x20005000 − 0xC = **0x20004FF4**.