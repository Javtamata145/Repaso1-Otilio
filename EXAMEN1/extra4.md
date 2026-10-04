# Ejercicios Día 4: Direccionamiento, formato de instrucción y ensamblador

**Temas:** modos de direccionamiento, valores inmediatos, ensamblador de AVR, PIC18 y ARM, formato de instrucción, microprocesador virtual y ortogonalidad.
**Tiempo sugerido:** 60 a 90 minutos.

---

## Ejercicios

**1.** Identifica el modo de direccionamiento del operando (inmediato, directo o indirecto por registro):
- a) `LDI R16, 0x25`
- b) `LDS R16, 0x0100`
- c) `LD R16, X`
- d) `MOVLW 0x30`
- e) `MOVWF 0x25`
- f) `MOVWF INDF0`
- g) `LDR R0, [R1]`
- h) `MOV AX, [BX]`
- i) `MOV AX, 5`

**2.** Explica si las siguientes instrucciones son correctas o no y di la razón:
- a) `LDI R10, 0x25` (AVR)
- b) `LDI R16, 0x1FF` (AVR)
- c) `MOVLW 0x1FF` (PIC18)
- d) `MOV AL, BX` (Intel)
- e) `MOV EAX, EBX` (Intel)
- f) `MOVW R0, #0x1234` (ARM Thumb-2)
- g) `MOVT R0, #0x12345` (ARM Thumb-2)
- h) `MOV [1000], [2000]` (Intel, memoria a memoria)
- i) `LDI R20, 0xFF` (AVR)

**3.** En el PIC18F4550, el registro W tiene un valor y se desea escribirlo en la dirección de RAM **0x5F2**. Escribe las instrucciones con direccionamiento directo y con indirecto. ¿En qué banco y con qué desplazamiento está la dirección 0x34C?

**4.** Escribe las instrucciones para cargar la constante **0x2FA7** en un registro interno del ATmega328P, del PIC18F4550 y del TM4C1294NCPDT.

**5.** En un ARM Thumb-2:
- a) Escribe dos instrucciones para cargar 0x12345678 en R4 usando `MOVW` y `MOVT`.
- b) Si R2 vale 0x0000CAFE y se ejecuta `MOVT R2, #0xBEEF`, ¿cuánto vale R2?

**6.** Explica por qué no existe direccionamiento directo en los microcontroladores ARM y escribe las instrucciones para leer en R0 el byte de la dirección 0x20000010.

**7.** Diseña el formato de una instrucción de **24 bits** para un microprocesador virtual de 16 registros con tres operandos de registro y un código de operación de 8 bits (los bits que sobren quedan sin usar, al final).
- a) ¿Cuántas instrucciones distintas puede tener?
- b) Codifica `ADD R3, R1, R2` si el opcode de ADD es 0x0A.
- c) ¿Para qué tipo de arquitectura está diseñada?

**8.** Un microprocesador virtual tiene instrucciones de 16 bits con el formato `[opcode 8 bits][Rd 4 bits][Rs 4 bits]`. Decodifica 0x0A4C y 0x1F29. Si el opcode 0x0A es `ADD Rd,Rs`, ¿qué hace 0x0A4C?

**9.** Di en cada caso si el conjunto de instrucciones es **ortogonal** o no y por qué:
- a) Cualquier instrucción puede usar cualquier registro y cualquier modo de direccionamiento.
- b) Solo el acumulador puede ser destino de una suma.
- c) `LDI` solo funciona con R16 a R31, pero el resto de instrucciones usa cualquier registro.
- d) Todas las instrucciones aritméticas aceptan operandos en registro o en memoria indistintamente.

**10.** Escribe el algoritmo a detalle para escribir **50 localidades** de RAM con el valor **0xFF**, empezando por la dirección más baja de RAM, para el ATmega328P (SRAM desde 0x0100), el PIC18F4550 (RAM desde 0x000) y el TM4C1294NCPDT (SRAM desde 0x20000000).

**11.** ¿Qué es un valor inmediato? Da un ejemplo en AVR y otro en PIC18. ¿Por qué `LDI R10, 0x25` no es válida en AVR?

**12.** Una instrucción de 32 bits debe tener un opcode y **tres operandos de registro** en un procesador con **32 registros**. ¿Cuántos bits ocupan los operandos? ¿Cuántos quedan para el opcode? ¿Cuántas instrucciones distintas puede codificar?

---

## Respuestas

**1.** a) inmediato; b) directo; c) indirecto por registro (X); d) inmediato; e) directo; f) indirecto (por FSR0); g) indirecto por registro; h) indirecto por registro; i) inmediato.

**2.**
- a) **Incorrecta**: `LDI` solo trabaja con R16 a R31.
- b) **Incorrecta**: 0x1FF necesita 9 bits y el campo de LDI es de 8 bits (máximo 0xFF).
- c) **Incorrecta**: el literal de MOVLW es de 8 bits.
- d) **Incorrecta**: AL es de 8 bits y BX de 16 (tamaños distintos).
- e) **Correcta**: ambos de 32 bits.
- f) **Correcta**: `MOVW` carga un valor de 16 bits.
- g) **Incorrecta**: 0x12345 tiene más de 16 bits.
- h) **Incorrecta**: en x86 no se puede de memoria a memoria en una sola instrucción.
- i) **Correcta**: R20 está en R16 a R31 y 0xFF cabe en 8 bits.

**3.** 0x5F2 = banco 5, desplazamiento 0xF2.
```asm
; Directo
MOVLB 0x05
MOVWF 0xF2, BANKED

; Indirecto
LFSR  0, 0x5F2
MOVWF INDF0
```
0x34C = banco **3**, desplazamiento **0x4C**.

**4.**
- ATmega328P (registros de 8 bits, se usan dos): `LDI R17, 0x2F` y `LDI R16, 0xA7`.
- PIC18F4550: `MOVLW 0x2F`, `MOVWF REGH`, `MOVLW 0xA7`, `MOVWF REGL`.
- TM4C1294NCPDT: `MOVW R0, #0x2FA7` (o `LDR R0, =0x2FA7`).

**5.**
- a) `MOVW R4, #0x5678` y `MOVT R4, #0x1234`.
- b) `MOVT` escribe los 16 bits altos y deja los bajos: **0xBEEFCAFE**.

**6.** Las instrucciones de ARM tienen 32 bits (16 o 32 en Thumb-2), así que una dirección completa de 32 bits no cabe en la instrucción junto con el opcode. Se carga la dirección en un registro y se accede de forma indirecta:
```asm
LDR  R1, =0x20000010
LDRB R0, [R1]
```

**7.** Formato: `opcode (8) | Rd (4) | Rs1 (4) | Rs2 (4) | sin usar (4)`.
- a) 2^8 = **256** instrucciones.
- b) `ADD R3,R1,R2` = `0A | 3 | 1 | 2 | 0` = `00001010 0011 0001 0010 0000` = **0x0A3120**.
- c) Arquitectura de **registros de propósito general** con tres operandos.

**8.**
- 0x0A4C → opcode 0x0A, Rd = 0x4 = R4, Rs = 0xC = R12. Como 0x0A es ADD: **R4 ← R4 + R12**.
- 0x1F29 → opcode 0x1F, Rd = R2, Rs = 0x9 = R9.

**9.** a) **Ortogonal**. b) **No ortogonal** (el acumulador tiene un papel especial). c) **No completamente ortogonal** (LDI tiene una restricción de registros). d) **Ortogonal** en cuanto a modos de operando.

**10.**
```asm
; ATmega328P
    ldi  XH, 0x01
    ldi  XL, 0x00        ; X = 0x0100
    ldi  r16, 50         ; contador
    ldi  r17, 0xFF       ; valor
lazo: st X+, r17
    dec  r16
    brne lazo

; PIC18F4550  (se usa FSR0L como contador porque la RAM empieza en 0x000)
    LFSR  0, 0x000
lazo: SETF POSTINC0      ; escribe 0xFF y avanza
    MOVLW d'50'
    CPFSEQ FSR0L         ; salta si FSR0L == 50
    BRA   lazo

; TM4C1294NCPDT
    LDR  R0, =0x20000000
    MOV  R1, #50
    MOV  R2, #0xFF
lazo: STRB R2, [R0], #1
    SUBS R1, R1, #1
    BNE  lazo
```

**11.** Es una constante que va escrita dentro de la propia instrucción. AVR: `LDI R16, 0x25`. PIC18: `MOVLW 0x25`. `LDI R10, 0x25` no es válida porque `LDI` solo trabaja con los registros R16 a R31.

**12.** 3 × 5 bits (32 registros = 2^5) = **15 bits** de operandos. Quedan 32 − 15 = **17 bits** para el opcode. Instrucciones distintas: 2^17 = **131,072**.