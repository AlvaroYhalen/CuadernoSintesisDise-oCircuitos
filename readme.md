<div align="center">

# 📘 Cuaderno de Síntesis · Unidad 1
### Análisis de Lógica Combinacional con Diseño Clásico

**Diseño de Circuitos** · Carrera de Computación · 2.º ciclo, paralelo A

<img width="500" height="161" alt="image" src="https://github.com/user-attachments/assets/08db7c73-bf0c-423e-99d4-5ef79a532b3a" />



**Universidad Nacional de Loja** · Período académico septiembre 2026 – marzo 2027

![Unidad](https://img.shields.io/badge/Unidad-1-blue) ![Semanas](https://img.shields.io/badge/Semanas-1%20a%204-green) ![Resultado](https://img.shields.io/badge/Resultado-R1-orange) ![Estado](https://img.shields.io/badge/Estado-En%20construcci%C3%B3n-yellow)

</div>

---

## 🪪 Portada

| | |
|---|---|
| 👤 **Estudiante** | `ALVARO YHALEN VILLAFUERTE CONDOY ` |
| 🎓 **Carrera / Ciclo** | Computación · 2.º ciclo · Paralelo A |
| 📚 **Asignatura** | Diseño de Circuitos (código institucional E2C2A1) |
| 👨‍🏫 **Docente** | Ing. Luis Darío Sinche Cueva, Mg. |
| 🗓️ **Período** | Septiembre 2026 – marzo 2027 |

---

## 🧭 Menú de navegación

| | Sección | Enlace |
|:-:|---|---|
| 🎯 | Resultado de aprendizaje y ruta de la unidad | [Ir](#objetivo) |
| 1️⃣ | Sistemas numéricos, códigos y compuertas | [Ir](#semana-1) |
| 2️⃣ | Álgebra de Boole y formas canónicas | [Ir](#semana-2) |
| 3️⃣ | Mapas de Karnaugh, indiferentes y NAND/NOR | [Ir](#semana-3) |
| 4️⃣ | Circuitos aritméticos | [Ir](#semana-4) |
| 🧩 | Mapa conceptual de la unidad | [Ir](#mapa) |
| 📖 | Glosario | [Ir](#glosario) |
| 🔗 | Referencias | [Ir](#referencias) |
| 🗂️ | Estructura del repositorio | [Ir](#estructura) |

---

<a id="objetivo"></a>
## 🎯 Resultado de aprendizaje y ruta de la unidad

> **R1.** Diseña e implementa circuitos combinacionales básicos utilizando técnicas de diseño clásico, bajo los principios de solidaridad, transparencia, responsabilidad y honestidad.

**Procedimiento de diseño clásico** que se repite en toda la unidad:

`Enunciado` ➜ `Tabla de verdad` ➜ `Expresión (canónica)` ➜ `Minimización` ➜ `Esquema de compuertas` ➜ `Simulación y verificación`

| Semana | Tema | Idea central |
|:-:|---|---|
| 1️⃣ | Sistemas numéricos, códigos y compuertas | Todo se reduce a dos estados y a siete compuertas |
| 2️⃣ | Álgebra de Boole y formas canónicas | Un circuito y una expresión son la misma cosa |
| 3️⃣ | Mapas de Karnaugh y NAND/NOR | Minimizar de forma visual y construir con una sola familia |
| 4️⃣ | Circuitos aritméticos | Un circuito sin memoria puede sumar, restar y comparar |

---

<a id="semana-1"></a>
## 1️⃣ Semana 1 · Sistemas numéricos, códigos y compuertas lógicas

**🎯 Objetivo:** convertir entre bases numéricas, representar negativos en complemento a dos, reconocer los códigos BCD, Gray y ASCII, y leer las compuertas lógicas en un circuito integrado 74LS.

### ⚡ 1.1 Representación binaria

- Un **transistor** actúa como interruptor controlado por voltaje; con solo dos estados es fácil distinguirlos aun con ruido.
- Un «1» o un «0» **no es un voltaje exacto, sino un rango**. En la familia **74LS**:

| Nivel | Salida (garantiza) | Entrada (interpreta) |
|---|:-:|:-:|
| 1 lógico | ≥ 2,7 V | ≥ 2,0 V |
| 0 lógico | ≤ 0,5 V | ≤ 0,8 V |
| Zona indefinida | — | entre 0,8 V y 2,0 V |

- **Margen de ruido:** alto = 2,7 − 2,0 = **0,7 V**; bajo = 0,8 − 0,5 = **0,3 V**.
- ⚠️ Una entrada sin conectar puede caer en la zona indefinida y producir lecturas erróneas.

### 🔢 1.2 Sistemas numéricos

En un sistema **posicional**, cada posición vale una potencia de la base.

| Sistema | Base | Observación |
|---|:-:|---|
| Decimal | 10 | Dígitos 0 a 9 |
| Binario | 2 | Pesos 128, 64, 32, 16, 8, 4, 2, 1. 1 bit = un dígito binario; 1 byte = 8 bits |
| Octal | 8 | Agrupa el binario de **3 en 3 bits** |
| Hexadecimal | 16 | Agrupa el binario de **4 en 4 bits** (A=10 … F=15) |

**Conversiones**
- **Binario ➜ decimal:** sumar los pesos de las posiciones en 1. Ejemplo: `1011₂ = 8 + 2 + 1 = 11`.
- **Decimal ➜ binario:** dividir sucesivamente entre 2 y leer los restos de abajo hacia arriba. Ejemplo: `25 = 11001₂`.
- **Binario ➜ hexadecimal/octal:** agrupar bits desde la derecha. Ejemplo: `157 = 10011101₂ = 9D₁₆ = 235₈`.

### ➕ 1.3 Aritmética binaria y complemento a dos

- **Suma binaria:** `0+0=0`, `0+1=1`, `1+1=10` (se escribe 0 y se lleva 1), `1+1+1=11`.
- **Complemento a dos:** convención para representar negativos; el bit de la izquierda indica el signo (0 positivo, 1 negativo).
  - Con 4 bits el rango es **−8 a +7**; con 8 bits, **−128 a +127**.
  - **Obtener −X:** invertir los bits de X y sumar 1. Ejemplo: `3 = 0011 → 1100 → 1101 = −3`.
  - **Ventaja:** restar es sumar el negativo (`A − B = A + (−B)`); basta un sumador más inversores. El bit sobrante a la izquierda se descarta.
- **Desbordamiento (overflow):** ocurre cuando el resultado no cabe en los bits disponibles (por ejemplo, `0111 + 0001 = 1000 = −8` en 4 bits). Se detecta con hardware en la semana 4.

### 🔤 1.4 Códigos

| Código | Descripción | Uso típico |
|---|---|---|
| **BCD** | Cada dígito decimal en 4 bits (157 ➜ `0001 0101 0111`); las combinaciones 1010 a 1111 no se usan | Displays, relojes, contadores |
| **Gray** | Entre valores consecutivos cambia **un solo bit**; se genera con el método del espejo | Encoders rotativos; orden de filas y columnas del mapa de Karnaugh |
| **ASCII** | Tabla de 7 bits (128 caracteres) que asigna un número a cada carácter; «A» = 65 = `01000001` | Representación de texto (la ñ y las tildes requieren UTF-8) |

### 🚪 1.5 Compuertas lógicas


<img width="333" height="399" alt="image" src="https://github.com/user-attachments/assets/f09413a9-4500-4141-b4b6-fef5a76be238" />


| Compuerta | Expresión | Salida en 1 cuando… |
|---|:-:|---|
| **NOT** | `Y = A'` | La entrada es 0 (invierte) |
| **AND** | `Y = A·B` | **Todas** las entradas valen 1 |
| **OR** | `Y = A+B` | **Al menos una** entrada vale 1 |
| **NAND** | `Y = (A·B)'` | **No** todas las entradas valen 1 |
| **NOR** | `Y = (A+B)'` | **Ninguna** entrada vale 1 |
| **XOR** | `Y = A⊕B` | Las entradas son **distintas** |
| **XNOR** | `Y = (A⊕B)'` | Las entradas son **iguales** |

- El círculo en la salida de un símbolo significa «negado».
- Existen dos normas de dibujo (ANSI y rectangular); el curso usa **ANSI**.

### 🔌 1.6 Circuitos integrados 74LS y hoja de datos

- Las compuertas se comercializan en circuitos integrados; el **74LS08** contiene 4 compuertas AND de 2 entradas en encapsulado **DIP-14**.
- **Pines:** muesca arriba, pin 1 arriba a la izquierda y conteo en sentido antihorario; alimentación **+5 V en el pin 14** y **tierra en el pin 7**.
- **Lectura del código** `SN 74 LS 08 N`: fabricante (Texas Instruments) · rango comercial · familia TTL · función (4 AND) · encapsulado plástico. Una versión 74HC08 cumple la misma función y pines en tecnología CMOS.
- La información completa se obtiene en la **hoja de datos** del fabricante.

---

<a id="semana-2"></a>
## 2️⃣ Semana 2 · Álgebra de Boole y formas canónicas

**🎯 Objetivo:** pasar de un enunciado a la tabla de verdad, a la forma canónica y a un circuito simplificado.

### 🔁 2.1 Circuito = expresión

| Circuito | Expresión |
|---|---|
| Cable de entrada | Variable (A, B, C) |
| AND | Producto `·` |
| OR | Suma `+` |
| NOT | Complemento `'` |
| Salida | Valor de la expresión |

Precedencia de operadores: **NOT ➜ AND ➜ OR**. Ejemplo: `Y = A·B + C'`.

### 📝 2.2 Del enunciado a la especificación

Traducir un enunciado en lenguaje natural exige eliminar ambigüedades. «La sirena suena cuando se activan dos sensores» admite dos lecturas: *exactamente dos* (`Σm(3,5,6)`) o *al menos dos* (`Σm(3,5,6,7)`). La especificación debe fijar una sola.

### 📐 2.3 Postulados y teoremas del álgebra de Boole

Se trabaja sobre el conjunto {0, 1} con las operaciones `+`, `·` y `'`. El principio de **dualidad** indica que al intercambiar `+` con `·` y `0` con `1` (sin complementar variables) la identidad sigue siendo válida.

| Postulado | Forma OR | Forma AND (dual) |
|---|---|---|
| Identidad | `X + 0 = X` | `X · 1 = X` |
| Complemento | `X + X' = 1` | `X · X' = 0` |
| Conmutativa | `X + Y = Y + X` | `XY = YX` |
| Distributiva | `X(Y+Z) = XY + XZ` | `X + YZ = (X+Y)(X+Z)` |

| Teorema | Forma OR | Forma AND |
|---|---|---|
| Elemento nulo | `X + 1 = 1` | `X · 0 = 0` |
| Idempotencia | `X + X = X` | `X · X = X` |
| Involución | `(X')' = X` | |
| Absorción | `X + XY = X` | `X(X+Y) = X` |
| Absorción del complemento | `X + X'Y = X + Y` | `X(X'+Y) = XY` |
| Adyacencia | `XY + XY' = X` | `(X+Y)(X+Y') = X` |
| Consenso | `XY + X'Z + YZ = XY + X'Z` | `(X+Y)(X'+Z)(Y+Z) = (X+Y)(X'+Z)` |

### 🔀 2.4 Leyes de De Morgan

> **«Rompe la barra, cambia el operador».**

- `(A·B)' = A' + B'`
- `(A+B)' = A'·B'`
- Se generaliza a n variables: `(A+B+C)' = A'B'C'`.

### 🧮 2.5 Minitérminos y maxitérminos

| | Minitérmino `mᵢ` | Maxitérmino `Mᵢ` |
|---|---|---|
| Tipo | **Producto** de todas las variables | **Suma** de todas las variables |
| Vale | 1 en una sola fila | 0 en una sola fila |
| Regla | Variable en 1 ➜ sin complemento; en 0 ➜ complementada | Variable en 0 ➜ sin complemento; en 1 ➜ complementada |
| Relación | | `Mᵢ = (mᵢ)'` |

### 🧱 2.6 Formas canónicas

| Forma | Se leen las filas con… | Se unen mediante… | Notación |
|---|:-:|:-:|:-:|
| **SOP** (suma de productos) | F = **1** | OR de minitérminos | `Σm(...)` |
| **POS** (producto de sumas) | F = **0** | AND de maxitérminos | `ΠM(...)` |

- Los índices de `ΠM` son los que **faltan** en `Σm`.
- La forma canónica **siempre existe y es única**.
- **Criterio de elección:** pocos 1 ➜ SOP; pocos 0 ➜ POS; solo NAND ➜ SOP (NAND-NAND); solo NOR ➜ POS (NOR-NOR). El criterio final es el **costo** (compuertas, circuitos integrados y niveles lógicos).

### ✂️ 2.7 Simplificación algebraica

Procedimiento: (1) agrupar pares adyacentes `XY + XY' = X`; (2) duplicar términos si hace falta `X = X + X`; (3) absorción; (4) absorción del complemento; (5) consenso.

> **Ejemplo de referencia (alarma de 3 sensores, «al menos dos»):**
> `F = Σm(3,5,6,7) = A'BC + AB'C + ABC' + ABC` ➜ `F = AB + AC + BC`
> Reduce el costo de **4 CI** (versión canónica) a **2 CI** (7408 + 7432).

⚠️ **Limitación:** el álgebra no indica cuándo se alcanzó la expresión mínima; esto motiva los mapas de Karnaugh.

---

<a id="semana-3"></a>
## 3️⃣ Semana 3 · Mapas de Karnaugh, condiciones indiferentes y NAND/NOR

**🎯 Objetivo:** obtener la expresión mínima en SOP y POS mediante mapas de Karnaugh, tratar las condiciones indiferentes e implementar con una sola familia de compuertas.

### 🗺️ 3.1 Fundamento: teorema de adyacencia

`XY + XY' = X` ➜ si dos minitérminos difieren en **una sola variable**, esa variable desaparece. El mapa de Karnaugh es una disposición geométrica de la tabla de verdad que hace visibles esas adyacencias.

### 🔢 3.2 ¿Por qué el orden 00, 01, 11, 10?

Se utiliza **código Gray** en filas y columnas, de modo que celdas vecinas difieren en un solo bit. Además, **el mapa se enrolla**: la última celda es vecina de la primera.

| Mapa | Distribución de minitérminos |
|---|---|
| **3 variables** (A \ BC, columnas 00-01-11-10) | Fila A=0: `0 1 3 2` · Fila A=1: `4 5 7 6` |
| **4 variables** (AB \ CD, ambos en Gray) | `0 1 3 2` / `4 5 7 6` / `12 13 15 14` / `8 9 11 10` |

### 📏 3.3 Reglas de agrupación

1. **Tamaño 2ᵏ** (1, 2, 4, 8 o 16 celdas); un grupo de 2ᵏ celdas elimina *k* variables.
2. **Rectangular:** sin formas en L ni diagonales.
3. **Lo más grande posible:** grupos grandes generan términos más cortos.
4. **El mapa se enrolla:** bordes opuestos y esquinas son vecinos (por ejemplo, las 4 esquinas forman `B'D'`).

**Lectura de un grupo:** se conservan solo las variables que **no cambian**. Constante en 1 ➜ `A`; constante en 0 ➜ `A'`; si cambia ➜ desaparece.

### ⭐ 3.4 Implicantes y procedimiento de minimización

| Concepto | Definición |
|---|---|
| **Implicante** | Cualquier grupo válido de 1 (o X) |
| **Implicante primo** | Grupo que ya no se puede agrandar |
| **Primo esencial** | Único primo que cubre algún 1; debe estar en la solución |

**Solución mínima = primos esenciales + los primos mínimos necesarios para cubrir el resto.**
Pasos: **Colocar** 1, 0 y X ➜ **Agrupar** los más grandes ➜ **Elegir** primos esenciales ➜ **Cubrir** los 1 restantes ➜ **Leer** un término por grupo. La solución mínima no siempre es única.

### 🔄 3.5 SOP y POS en el mapa

- **SOP:** se agrupan los **1** y se lee directamente.
- **POS:** se agrupan los **0** y la lectura es **invertida** (0 ➜ `A`, 1 ➜ `A'`), con suma dentro de cada factor.
- **Ejemplo de referencia:** `F = Σm(0,1,2,5,8,9,10)`
  - SOP: `B'C' + B'D' + A'C'D` ➜ 7 literales
  - POS: `(A'+B')(B'+D)(C'+D')` ➜ 6 literales
- **Criterio:** construir ambas y elegir la de menor costo en literales, compuertas y circuitos integrados.

### ❎ 3.6 Condiciones indiferentes (X)

Son combinaciones que **nunca ocurren** (por ejemplo, en BCD las combinaciones 1010 a 1111). Notación: `F = Σm(...) + d(...)`.

| Regla | Descripción |
|---|---|
| ✅ Como **1** | Si agranda un grupo, se incluye: el término queda más corto |
| ✅ Como **0** | Si no ayuda, se ignora: ninguna X está obligada a quedar cubierta |
| 🚫 **Nunca sola** | Un grupo formado solo por X agrega un término inútil |

> **Ejemplo (dígito BCD ≥ 5):** `F = Σm(5,6,7,8,9) + d(10…15)`. Sin usar las X: `AB'C' + A'BD + A'BC` (9 literales). Usándolas: **`A + BD + BC`** (5 literales).

### 🧩 3.7 Universalidad de NAND y NOR

Con **solo NAND** (o **solo NOR**) se puede construir cualquier función.

| Función | Solo NAND | Solo NOR |
|---|:-:|:-:|
| NOT | `(A·A)'` | `(A+A)'` |
| AND | `((AB)')'` | `(A'+B')'` |
| OR | `(A'·B')'` | `((A+B)')'` |

**Conversión de esquemas:** **SOP mínima ➜ NAND-NAND** y **POS mínima ➜ NOR-NOR**. Se aplica doble negación y De Morgan; el **literal que aparece solo se complementa** (NAND usada como inversor). Se mantienen dos niveles, por lo que el retardo es igual al de AND-OR.

**Costo en circuitos integrados** (ejemplo BCD ≥ 5): sin X ➜ 3 CI (7404 + 7411 + 7432); con X, AND-OR ➜ 2 CI (7408 + 7432); con X, solo NAND ➜ 2 CI (7400 + 7410). El ahorro proviene de las X; la NAND unifica la familia de compuertas en el inventario.

---

<a id="semana-4"></a>
## 4️⃣ Semana 4 · Circuitos aritméticos

**🎯 Objetivo:** diseñar con el procedimiento clásico un sumador de 4 bits, utilizarlo también para restar y estimar su tiempo de respuesta. Es la base de la **ALU** de un procesador.

### 1️⃣ 4.1 Suma de un bit

`S` = dígito que se escribe · `C` = acarreo («me llevo»). Un acarreo puede provocar otro, por lo que los acarreos se **encadenan**.

### ➕ 4.2 Semisumador (columna 0)

Suma **2 bits** (A y B); no recibe acarreo.

| A | B | C | S |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 0 |

**`S = A ⊕ B`** (XOR) · **`C = A · B`** (AND)

### ➕➕ 4.3 Sumador completo (columnas 1, 2, 3…)

Suma **3 bits**: A, B y el acarreo de entrada `Cin`. Se construye contando los unos de cada fila y escribiendo el resultado en binario (`Cout S`).

| Salida | En palabras | Expresión |
|---|---|---|
| **S** | 1 cuando hay un número **impar** de unos | `S = A ⊕ B ⊕ Cin` (en el mapa, distribución de «tablero de ajedrez») |
| **Cout** | 1 cuando hay **al menos dos** unos | `Cout = AB + A·Cin + B·Cin` (tres grupos de dos) |

**Procedimiento:** tabla de verdad ➜ mapa de Karnaugh ➜ expresión y su lectura en palabras.

### 🌊 4.4 Sumador paralelo de 4 bits (ripple carry)

- Cuatro sumadores completos en cadena; regla única: **`Cout` de un sumador ➜ `Cin` del siguiente**.
- El acarreo avanza etapa por etapa, de derecha a izquierda, como una ola.
- **Estimación del retardo:** si cada compuerta tarda ≈ 10 ns y el acarreo cruza ≈ 2 compuertas por etapa, entonces **retardo ≈ 2 · n · 10 ns**.

| Bits (n) | Compuertas | Tiempo aproximado |
|:-:|:-:|:-:|
| 4 | 8 | 80 ns |
| 16 | 32 | 320 ns |
| 32 | 64 | 640 ns |

Más bits implican un circuito más lento.

### ➖ 4.5 Resta con el mismo sumador

- `A − B = A + (−B)`, y `−B` = invertir los bits de B y sumar 1.
- **Sumador/restador:** una compuerta **XOR** actúa como inversor controlado por una señal **M**.

| M | Efecto sobre B | Operación |
|:-:|---|---|
| 0 | B pasa igual | **Suma** |
| 1 | B se invierte (y `Cin` = 1 aporta el +1) | **Resta** |

Un único circuito suma o resta según M.

### 🚨 4.6 Desbordamiento (overflow)

- Con 4 bits y signo, el rango es −8 a +7; `0101 (+5) + 0100 (+4) = 1001 (−7)` ✗.
- Hay overflow si el acarreo que **entra** a la última etapa es distinto del que **sale**: **`V = C3 ⊕ C4`**.
- ⚠️ `Cout = 1` **no** implica error por sí solo.

### ⚖️ 4.7 Comparador de magnitud

- **¿A = B?** XNOR en cada bit (1 si son iguales) y AND de todas las salidas.
- **¿A > B?** Se compara desde el bit más significativo: el primer bit en que difieren decide. Circuito integrado de referencia: **7485**.

### 🧠 4.8 Relación con la ALU

La ALU de un procesador combina: **sumador/restador**, **comparador**, **compuertas AND/OR/XOR** y un **multiplexor** (semana 5) que selecciona el resultado de la instrucción.

---

<a id="mapa"></a>
## 🧩 Mapa conceptual de la unidad

```text
Sistemas numéricos y códigos (S1)
        │
        ▼
Compuertas y tablas de verdad (S1) ──► Álgebra de Boole, SOP/POS (S2)
                                                │
                                                ▼
                               Mapas de Karnaugh e indiferentes (S3)
                                                │
                                                ▼
                               NAND/NOR: implementación con una familia (S3)
                                                │
                                                ▼
                       Bloques aritméticos: sumadores, resta, comparador (S4)
                                                │
                                                ▼
                                   Hacia la ALU (S5 en adelante)
```

---

<a id="glosario"></a>
## 📖 Glosario

| Término | Definición |
|---|---|
| **Bit / Byte** | Dígito binario / conjunto de 8 bits |
| **Margen de ruido** | Diferencia de voltaje que tolera una señal antes de leerse mal |
| **Complemento a dos** | Convención para representar enteros con signo en binario |
| **Overflow** | Resultado que no cabe en los bits disponibles |
| **Minitérmino / Maxitérmino** | Producto / suma que contiene todas las variables y vale 1 / 0 en una sola fila |
| **SOP / POS** | Suma de productos / producto de sumas |
| **Implicante primo** | Grupo válido del mapa que no puede agrandarse |
| **Condición indiferente** | Combinación que nunca ocurre y puede usarse como 0 o 1 según convenga |
| **Acarreo (carry)** | Dígito que se lleva a la columna siguiente en una suma |
| **Ripple carry** | Sumador en el que el acarreo se propaga etapa por etapa |
| **ALU** | Unidad aritmético-lógica del procesador |

---

<a id="referencias"></a>
## 🔗 Referencias

Bibliografía citada en el sílabo de la asignatura y en las diapositivas del docente:

- Carpinelli, J. D. (2023). *An Animated Introduction to Digital Logic Design*. New Jersey Institute of Technology. ISBN 978-1-970194-005. *(Texto base)*
- Bégin, G. (2023). *Circuits logiques combinatoires et séquentiels*. *(Bibliografía básica virtual)*
- Garza, J. Á. (2025). *Electrónica digital I, Sistemas digitales*. Nuevo León. *(Recurso de Internet; lectura de la semana 2)*
- Universidad Nacional de Loja. (2026). *Sílabo de la asignatura Diseño de Circuitos*. Carrera de Computación.
- Sinche Cueva, L. D. (2026). *Diapositivas de clase, Unidad 1, semanas 1 a 4*. Diseño de Circuitos, Universidad Nacional de Loja.

---

<a id="estructura"></a>
## 🗂️ Estructura del repositorio

```text
cuaderno-diseno-circuitos-u1/
├── 📄 README.md   → Cuaderno de síntesis completo (semanas 1 a 4)
└── 🧭 MENU.md     → Menú de acceso rápido al cuaderno
```

<div align="center">

⬆️ [Volver al inicio](#-cuaderno-de-síntesis--unidad-1)

</div>
