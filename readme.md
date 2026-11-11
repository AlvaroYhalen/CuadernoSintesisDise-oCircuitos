<div align="center">

# 📓 Cuaderno de Síntesis · Unidad 1
## ⚡ Lógica Combinacional con Diseño Clásico

**📘 Asignatura:** Diseño de Circuitos (E2C2A1) · **🏛️ UNL** · Carrera de Computación  
**🎓 Ciclo:** 2 · **Paralelo:** A · **📅 Período:** sep 2026 – mar 2027  
**👨‍🏫 Docente:** Ing. Luis Darío Sinche Cueva, Mg.  
**🙋 Estudiante:** [Nombre completo]

</div>

---

## 🧭 Menú

| | | |
|---|---|---|
| [1️⃣ Números y compuertas](#semana-1) | [2️⃣ Álgebra de Boole](#semana-2) | [3️⃣ Karnaugh y NAND/NOR](#semana-3) |
| [4️⃣ Circuitos aritméticos](#semana-4) | [5️⃣ Mux y decodificadores](#semana-5) | [6️⃣ Cierre y método](#semana-6) |
| [📚 Referencias](#referencias) | | |

> 🎯 **Resultado R1:** diseñar e implementar circuitos combinacionales básicos con técnicas de diseño clásico. [7]  
> 💡 **Circuito combinacional** = la salida depende **solo de las entradas actuales** (sin memoria).

### 🔄 Método de la unidad

`Enunciado` ➜ `Tabla de verdad` ➜ `Σm / ΠM` ➜ `Minimizar (Karnaugh)` ➜ `Esquema` ➜ `Simular y comparar con la tabla`

---

<a id="semana-1"></a>
# 1️⃣ Semana 1 · Números, códigos y compuertas

### 🔌 ¿Por qué solo 0 y 1?
Un transistor es un interruptor controlado por voltaje; con dos estados es fácil distinguir uno del otro aunque haya ruido. [8]

| Familia 74LS | Salida garantizada | Entrada que lee |
|---|---|---|
| **1** | ≥ 2,7 V | ≥ 2,0 V |
| **0** | ≤ 0,5 V | ≤ 0,8 V |

⚠️ Entre 0,8 y 2,0 V hay una **zona indefinida** (típico error: entrada sin conectar). Márgenes de ruido: **0,7 V** (alto) y **0,3 V** (bajo).

### 🔢 Bases y conversiones
- **Binario → decimal:** suma de pesos (128 · 64 · 32 · 16 · 8 · 4 · 2 · 1).
- **Decimal → binario:** dividir entre 2 y leer los restos de abajo hacia arriba.
- **Hex = grupos de 4 bits · Octal = grupos de 3 bits** (desde la derecha).

> Ejemplo: `157 = 10011101₂ = 9D₁₆ = 235₈`

### ➖ Complemento a dos
- **Negativo = invertir bits + 1.** Rango en 4 bits: −8 a +7.
- **Restar = sumar el negativo:** `5 − 3 = 0101 + 1101 = 0010` (se descarta el acarreo final).
- ⚠️ **Desbordamiento:** `0111 + 0001 = 1000` (¡−8!). Pasa también con `int` en Java.

### 🔤 Códigos
| Código | Idea | Uso |
|---|---|---|
| **BCD** | cada dígito decimal en 4 bits (1010–1111 no se usan) | displays, relojes |
| **Gray** | entre vecinos cambia **un solo bit** | encoders, mapas de Karnaugh |
| **ASCII** | 7 bits = 128 caracteres (`A` = 65 = `01000001`) | texto |

### 🚪 Las 7 compuertas
| Compuerta | Sale 1 cuando… |
|---|---|
| NOT `A'` | la entrada es 0 |
| AND `A·B` | **todas** valen 1 |
| OR `A+B` | **al menos una** vale 1 |
| NAND | no todas valen 1 |
| NOR | **ninguna** vale 1 |
| XOR `⊕` | las entradas son **distintas** |
| XNOR | las entradas son **iguales** |

🎨 Se usa simbología **ANSI/IEEE** (formas distintivas); IEC usa rectángulos.

### 🧩 Circuito integrado 74LS08
- **DIP-14**, muesca arriba, pin 1 arriba a la izquierda, conteo antihorario.
- 🔋 **Pin 14 = +5 V · Pin 7 = GND**.
- Código `SN 74 LS 08 N` → fabricante · rango comercial · familia TTL · **4 AND de 2 entradas** · DIP plástico.
- Un `74HC08` es la versión CMOS: misma función y pines.

✅ **Me llevo:** 0/1 son rangos de voltaje · complemento a dos = invertir + 1 · BCD display, Gray sensores, ASCII texto · cada chip se lee en su hoja de datos.

🔬 *Práctica APE 01: comprobar la tabla de verdad de cada compuerta en el simulador.*

---

<a id="semana-2"></a>
# 2️⃣ Semana 2 · Álgebra de Boole y formas canónicas

### 🔁 Circuito = expresión
`Y = A·B + C'` → AND = producto · OR = suma · NOT = complemento.  
**Precedencia:** NOT ➜ AND ➜ OR.

### 📜 Postulados y dualidad
Identidad `X+0=X`, complemento `X+X'=1`, conmutativa, distributiva.  
🪞 **Dualidad:** intercambia `+ ↔ ·` y `0 ↔ 1` y la igualdad sigue válida.  
⭐ La distributiva que sorprende: `A + BC = (A+B)(A+C)`.

### 🛠️ Teoremas útiles
| Teorema | Forma |
|---|---|
| Idempotencia | `X+X = X` |
| Absorción | `X + XY = X` |
| Absorción del complemento | `X + X'Y = X + Y` |
| Adyacencia | `XY + XY' = X` |
| Consenso | `XY + X'Z + YZ = XY + X'Z` |

### 🔀 De Morgan
> **"Rompe la barra, cambia el operador."**  
> `(AB)' = A' + B'` · `(A+B)' = A'·B'`

### 🧱 Minitérminos y maxitérminos
| | Minitérmino mᵢ | Maxitérmino Mᵢ |
|---|---|---|
| Operación | **producto** | **suma** |
| Vale | 1 solo en la fila i | 0 solo en la fila i |
| Variable en 1 / 0 | directa / complementada | complementada / directa |

Relación: `Mᵢ = (mᵢ)'`

### 📋 SOP vs POS
| | SOP (Σm) | POS (ΠM) |
|---|---|---|
| Lee las filas con | **F = 1** | **F = 0** |
| Une con | OR de minitérminos | AND de maxitérminos |
| Conviene si hay | pocos 1 | pocos 0 |
| Con solo… | NAND-NAND (7400) | NOR-NOR (7402) |

### 🚨 Ejemplo clave: alarma de 3 sensores
⚠️ *"Suena cuando se activan dos sensores"* es ambiguo: **exactamente dos** `Σm(3,5,6)` vs **al menos dos** `Σm(3,5,6,7)` (la que se pidió).

```text
F = Σm(3,5,6,7) = ΠM(0,1,2,4)
Simplificada:  F = AB + AC + BC      (POS: (A+B)(A+C)(B+C))
```

| Versión | Costo |
|---|---|
| Canónica | **4 CI** (7404 + 2×7411 + 7432) |
| Simplificada | **2 CI** (7408 + 7432) |

✅ **Me llevo:** la tabla manda (dos expresiones son equivalentes si tienen la misma tabla) · la forma canónica siempre existe y es única · simplificar ahorra hardware, pero el álgebra **no garantiza el mínimo**.

🔬 *Práctica APE 02: canónica vs simplificada y conteo de CI.*

---

<a id="semana-3"></a>
# 3️⃣ Semana 3 · Mapas de Karnaugh y NAND/NOR

### 🗺️ ¿Por qué un mapa?
Se basa en **adyacencia**: si dos minitérminos difieren en una variable, esa variable desaparece (`XY + XY' = X`).  
Por eso filas y columnas van en **código Gray: 00, 01, 11, 10**.

| AB \ CD | 00 | 01 | 11 | 10 |
|:---:|:---:|:---:|:---:|:---:|
| **00** | m0 | m1 | m3 | m2 |
| **01** | m4 | m5 | m7 | m6 |
| **11** | m12 | m13 | m15 | m14 |
| **10** | m8 | m9 | m11 | m10 |

### 📏 Reglas para agrupar
1. Tamaño **2ᵏ** (1, 2, 4, 8, 16): un grupo de 2ᵏ elimina **k** variables.
2. Solo **rectángulos** (nada de L ni diagonales).
3. Lo **más grandes** posible.
4. 🌀 **El mapa se enrolla:** bordes opuestos y las 4 esquinas son vecinos.

**Leer un grupo:** se conservan las variables que **no cambian** (1 → `A`, 0 → `A'`).

### 🏅 Implicantes
- **Primo:** grupo que ya no se puede agrandar.
- **Esencial:** único primo que cubre algún 1 → **debe** estar en la solución.
- **Mínimo** = esenciales + los primos mínimos para cubrir el resto.

### ✅ Ejemplo: `F = Σm(0,1,2,5,8,9,10)`
`F = B'C' + B'D' + A'C'D` → 3 términos, **7 literales**  
(esquinas = `B'D'`, bordes superior/inferior = `B'C'`).

**En POS (se agrupan los 0 y se lee invertido):**  
`F = (A'+B')(B'+D)(C'+D')` → **6 literales** 🏆  
👉 Se construyen ambas y se elige la de menor costo.

### ❌ Condiciones indiferentes (X)
| Si… | Entonces |
|---|---|
| agrandan un grupo | se usan como **1** |
| no ayudan | se ignoran (como 0) |
| formarían un grupo solas | **nunca** se agrupan |

**Ejemplo BCD ≥ 5:** `F = Σm(5…9) + d(10…15)`

| | Resultado | Literales |
|---|---|---|
| Sin usar las X | `AB'C' + A'BD + A'BC` | 9 |
| Con las X | `A + BD + BC` | **5** ✨ |

### 🔧 Universalidad NAND / NOR
| Función | Solo NAND | Solo NOR |
|---|---|---|
| NOT | `(A·A)'` | `(A+A)'` |
| AND | `((AB)')'` | `(A'+B')'` |
| OR | `(A'·B')'` | `((A+B)')'` |

- **SOP mínima → NAND-NAND** · **POS mínima → NOR-NOR**.
- **Conversión SOP → NAND:** doble negación + De Morgan; cada paréntesis es una NAND, y el literal solo entra **complementado** (NAND como inversor).

```text
F = A + BD + BC = NAND( A', NAND(B,D), NAND(B,C) )
```

| Implementación | CI |
|---|---|
| Sin X | 3 (7404 + 7411 + 7432) |
| Con X, AND-OR | 2 (7408 + 7432) |
| Con X, solo NAND | 2 (7400 + 7410) |

💡 El ahorro vino de las **X**; la NAND no agrega chips y deja **una sola familia** en el inventario.

✅ **Me llevo:** Gray + grupos grandes = términos cortos · primos esenciales primero · X solo si ayudan · la solución mínima no siempre es única.

🔬 *Práctica APE 03: circuito antes/después de minimizar y conversión a una familia.*

---

<a id="semana-4"></a>
# 4️⃣ Semana 4 · Circuitos aritméticos

> 🧠 Un circuito **sin memoria** suma, y el **acarreo** es su problema central. Es el corazón de la **ALU**.

### ➕ Semisumador (columna 0, 2 bits)
| Salida | Función | Compuerta |
|---|---|---|
| S (suma) | `A ⊕ B` | XOR |
| C (acarreo) | `A · B` | AND |

### ➕➕ Sumador completo (3 bits: A, B, Cin)
Truco: **cuenta los unos** de la fila y escríbelo en binario `Cout S`.

| Salida | En palabras | Expresión |
|---|---|---|
| **S** | número **impar** de unos | `A ⊕ B ⊕ Cin` (tablero de ajedrez en el K-map) |
| **Cout** | **al menos dos** unos | `AB + A·Cin + B·Cin` |

### 🌊 Sumador paralelo de 4 bits (ripple)
Se encadenan 4 sumadores: **Cout de uno → Cin del siguiente**. El resultado se completa de derecha a izquierda, como una ola.

⏱️ **Retardo ≈ 2 · n · 10 ns** (2 compuertas por etapa):

| Bits | Tiempo |
|:---:|:---:|
| 4 | 80 ns |
| 16 | 320 ns |
| 32 | 640 ns |

### ➖ Resta: `A − B = A + (−B)`
Un solo circuito suma **o** resta con una línea **M**:
- `B ⊕ M` (XOR = inversor controlado) y **Cin = M** (aporta el +1).
- **M = 0 → suma · M = 1 → resta.**

> Ejemplo: `0110 − 0011 = 0110 + 1101 = 1 0011 → 3` ✅

### 🚨 Overflow
- Con signo (4 bits: −8 a +7): `0101 + 0100 = 1001 = −7` ❌
- **V = C3 ⊕ C4** (el acarreo que entra a la última etapa ≠ el que sale).
- ⚠️ **Cout = 1 NO significa error.**

### ⚖️ Comparador de magnitud
- **A = B:** XNOR en cada bit y AND de todos.
- **A > B:** de izquierda a derecha, el primer bit distinto decide. (Integrado **7485**.)

### 🧩 Demostración: `0101 + 0011 = 1000` (8)
Sin signo: correcto · Con signo: overflow. (Integrado sumador: **7483**.)

✅ **Me llevo:** `S` = impar de unos · `Cout` = al menos dos · ripple = el acarreo marca el retardo · restar es sumar con XOR + Cin=1.

🔬 *Práctica APE 04: semisumador, sumador completo, paralelo de 4 bits y resta.*

---

<a id="semana-5"></a>
# 5️⃣ Semana 5 · Selección y codificación de datos

> 📌 Resumen basado en el contenido del sílabo [7] y el texto base [1][2].

| Bloque | Qué hace | Clave |
|---|---|---|
| 🔀 **Multiplexor (MUX)** | elige 1 de 2ⁿ entradas con n líneas de selección | `Y = S'·I0 + S·I1` (2:1) |
| 📡 **Demultiplexor** | lleva 1 entrada a 1 de 2ⁿ salidas | **dual** del MUX |
| 🔓 **Decodificador** | activa 1 de 2ⁿ salidas según el código | cada salida es un **minitérmino** |
| 🔒 **Codificador** | convierte la línea activa en código binario | con prioridad si hay varias activas |
| 🔢 **BCD → 7 segmentos** | enciende los segmentos `a–g` de un display | ánodo común vs cátodo común |

### ✨ MUX como generador de funciones
Un MUX de 2ⁿ canales implementa **cualquier función de n variables sin minimizar**: las variables van a las selecciones y cada entrada de datos se conecta a **0 o 1** según la tabla.

> Ejemplo: `F(A,B,C) = Σm(1,2,4,7)` en un MUX 8:1 → entradas `I1=I2=I4=I7=1`, el resto 0 (es `A⊕B⊕C`).

🧱 **Expansión:** 2 MUX 4:1 + 1 MUX 2:1 = MUX 8:1.

⚖️ **Compuertas vs. MUX:** con Karnaugh suele costar menos en funciones simples; con MUX no se minimiza y cambiar la función es solo recablear.

✅ **Me llevo:** MUX/DEMUX son duales · decodificador entrega minitérminos · elegir bloque o compuertas es una decisión de **costo**.

🔬 *Práctica APE 05: MUX de 4 fuentes, función con MUX y display de 7 segmentos.*

---

<a id="semana-6"></a>
# 6️⃣ Semana 6 · Cierre de la unidad

📝 Evaluación sumativa (semanas 1–5) y 🚀 **primer avance del proyecto integrador:** especificación, tabla de verdad, expresión mínima y esquema combinacional simulado. [7]

### 🧰 ¿Qué técnica uso?
| Técnica | Ventaja | Límite |
|---|---|---|
| Canónica | directa y sistemática | muchas compuertas |
| Álgebra | sin dibujar mapas | no garantiza el mínimo |
| Karnaugh | mínimo garantizado | hasta 4 variables |
| NAND/NOR | una sola familia de chips | esquema menos legible |
| Multiplexor | sin minimizar | costo fijo del bloque |

### ⚠️ Errores frecuentes
1. Usar orden binario en vez de **Gray** en el mapa.
2. Grupos que **no** son potencia de 2.
3. Olvidar que el mapa **se enrolla**.
4. Agrupar X que no ayudan (o solas).
5. Confundir SOP con POS (en POS la lectura va **invertida**).
6. No contrastar la simulación con la **tabla de verdad**.
7. Creer que `Cout = 1` es overflow.

### ✅ Checklist de diseño
- [ ] Variables y tabla de verdad completa
- [ ] Σm / ΠM
- [ ] Expresión mínima justificada
- [ ] Esquema con integrados y pines
- [ ] Simulación = tabla de verdad
- [ ] Conteo de compuertas y CI

---

# 🤖 Declaración de uso de IA

| Herramienta | Finalidad | Verificación |
|---|---|---|
| [Herramienta] | [Ej.: organizar y resumir el cuaderno] | [Ej.: contraste con diapositivas, texto base y simulación] |

---

<a id="referencias"></a>
# 📚 Referencias (IEEE)

[1] J. D. Carpinelli, *An Animated Introduction to Digital Logic Design*. New Jersey: New Jersey Institute of Technology, 2023, ISBN 978-1-970194-005.

[2] G. Bégin, *Circuits logiques combinatoires et séquentiels*, 2023.

[3] J. Á. Garza, *Electrónica digital I, Sistemas digitales*. Nuevo León, 2025.

[4] Autodesk, "Tinkercad," 2023.

[5] MuseMaze, Inc., "EveryCircuit," 2025.

[6] CircuitLab, "CircuitLab," 2025.

[7] L. D. Sinche Cueva, "Sílabo de la asignatura Diseño de Circuitos," Universidad Nacional de Loja, 2026.

[8] L. D. Sinche Cueva, "Diapositivas de Diseño de Circuitos, Unidad 1, Semanas 1 a 4," Universidad Nacional de Loja, 2026.

---

<div align="center">

**📓 Cuaderno de Síntesis · Unidad 1 · Diseño de Circuitos · UNL · 2026**  
[⬆️ Volver al inicio](#-cuaderno-de-síntesis--unidad-1)

</div>
