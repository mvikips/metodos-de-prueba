# Apuntes de Álgebra y Matemática Discreta: Métodos de prueba, inducción y recursión

### **Por Mª Victoria Perera Sitzer**
*Facultad de Ingeniería, Tech Universidad Tecnológica • Clase del '22* 

---

El estudio de la lógica computacional y el álgebra discreta constituye la infraestructura invisible sobre la cual se erige todo el software moderno. Desde las restricciones de integridad en bases de datos relacionales hasta la verificación formal de algoritmos críticos, los conceptos de variables, cuantificadores, métodos de prueba, inducción y recursión estructuran nuestra capacidad para descomponer problemas complejos en soluciones verificables y deterministas.

---

## 1. Variables y Cuantificadores: El Lenguaje del Modelado Lógico

El término `variable` suele evocar interpretaciones diversas dependiendo del contexto. En el ámbito del álgebra y las matemáticas discretas, una variable es un símbolo abstracto que representa un conjunto de cantidades, relaciones o estructuras matemáticas.

A diferencia de la rigidez analítica tradicional, las variables presentan variabilidad de al menos tres formas distintas dentro del análisis de sistemas:

* **Variables que no varían (Incógnitas):** Actúan como marcadores de posición para valores fijos y específicos dentro de un contexto dado (por ejemplo, determinar el lado de un polígono regular a partir de su perímetro conocido). Al sustituirse, definen expresiones con un valor de verdad unívoco.
* **Variables discretas:** Aquellas cuyo dominio de discurso posee elementos aislados y contables, estructurables mediante matrices de adyacencia o tablas de correspondencia finitas.
* **Variables continuas:** Cambian de manera densa e ininterrumpida dentro de un intervalo real continuo.

De acuerdo con los marcos conceptuales de Usiskin y Juárez, los usos de la variable se corresponden directamente con la concepción estructural del álgebra aplicada:

| Concepción del Álgebra | Usos de la Variable |
| :--- | :--- |
| **Aritmética generalizada** | Generalizadores de patrones y regularidades |
| **Procedimientos de resolución** | Incógnitas, constantes del sistema |
| **Estudio de relaciones cuantitativas** | Argumentos de funciones, parámetros de control |
| **Estudio de estructuras puras** | Marcas arbitrarias abstractas en el papel |

### Cuantificadores Lógicos
Cuando un enunciado matemático o una restricción de software incluye variables sin instanciar, carece de un valor de verdad intrínseco; constituye un predicado o función proposicional $P(x)$. Para transformar esta función en una proposición válida sin evaluar caso por caso, empleamos los cuantificadores lógicos:

* **Cuantificador Universal ($\forall x$):** Dictamina que el predicado $P(x)$ es estrictamente verdadero para la totalidad de los elementos constituyentes del dominio de discurso.
* **Cuantificador Existencial ($\exists x$):** Preconiza que existe al menos un elemento en el dominio para el cual el predicado es verdadero.

Para el diseño avanzado de bases de datos, incorporamos el cuantificador de existencia única ($\exists !x$), el cual prescribe que uno y solo un elemento satisface la propiedad. Asimismo, las leyes de dualidad lógica determinan las equivalencias de su negación: negar la universalidad de una propiedad equivale a afirmar la existencia de un contraejemplo que la invalide de forma directa.

---

## 2. Métodos de Prueba y Reglas de Inferencia

Un teorema es una afirmación matemática cuya veracidad se demuestra mediante una secuencia lógica de pasos fundamentados en axiomas (principios evidentes no demostrados), hipótesis operacionales y teoremas previamente validados por la comunidad científica.

### Reglas de Inferencia Proposicional
Cada paso deductivo de una demostración formal debe justificarse mediante una regla de inferencia. Estas reglas se derivan directamente de tautologías lógicas fundamentales:

| Regla de Inferencia | Estructura Lógica (Tautología) |
| :--- | :--- |
| **Modus Ponens** | $[p \land (p \rightarrow q)] \rightarrow q$ |
| **Modus Tollens** | $[\neg q \land (p \rightarrow q)] \rightarrow \neg p$ |
| **Simplificación** | $(p \land q) \rightarrow p$ |
| **Silogismo Hipotético** | $[(p \rightarrow q) \land (q \rightarrow r)] \rightarrow (p \rightarrow r)$ |
| **Silogismo Disyuntivo** | $[(p \lor q) \land \neg p] \rightarrow q$ |

### Métodos de Demostración
Para verificar la validez de un condicional del tipo $p \rightarrow q$, la matemática discreta sistematiza los siguientes enfoques metodológicos:

* **Demostración Directa:** Se asume que la hipótesis $p$ es verdadera y, mediante la aplicación secuencial de reglas de inferencia, se infiere la veracidad de la tesis $q$.
* **Demostración por Contraposición (Indirecta):** Utiliza la equivalencia estructural $(p \rightarrow q) \equiv (\neg q \rightarrow \neg p)$. Se parte de la premisa de que la conclusión es falsa y se demuestra que, en consecuencia, la hipótesis también debe ser falsa.
* **Demostración por Contradicción (Reducción al Absurdo):** Se asume la negación directa de la sentencia que se pretende verificar. Si el desarrollo deductivo subsiguiente genera una inconsistencia formal (un absurdo lógico tipo $r \land \neg r$), la suposición inicial queda refutada, validando la tesis original.
* **Demostración por Casos:** Si la hipótesis está fragmentada en una disyunción de escenarios particulares ($p_1 \lor p_2 \lor \dots \lor p_n$), se demuestra la implicación de manera independiente para cada uno de los casos.
* **Demostración por Contraejemplo:** Diseñada para refutar de manera fulminante una afirmación de alcance universal ($\forall x P(x)$). Bastará con exhibir un único elemento del dominio donde el predicado sea falso.

---

## 3. Inducción Matemática: Escalando la Certeza al Infinito

El principio de inducción matemática es un método de demostración deductivo (no empírico) empleado para validar propiedades formuladas sobre conjuntos ordenados numerables, comúnmente los números enteros positivos ($\mathbb{Z}^+$).

La analogía clásica del efecto dominó ilustra con precisión su mecanismo lógico, el cual demanda obligatoriamente el cumplimiento de dos fases consecutivas:

1. **Caso Base (Verificación):** Demostrar mediante sustitución analítica directa que la proposición $P(n)$ es estrictamente verdadera para el primer elemento del dominio de interés (típicamente $n = 1$).
2. **Paso Inductivo:** Se asume como verdad transitoria que la propiedad se cumple para un entero arbitrario $k$ (esta premisa constituye la **Hipótesis Inductiva**). Bajo esta asunción, se debe demostrar rigurosamente que la propiedad es válida para el elemento inmediatamente siguiente: $k + 1$.

$$\left[ P(\text{base}) \land \forall k (P(k) \rightarrow P(k+1)) \right] \rightarrow \forall n P(n)$$

Si ambas condiciones se satisfacen de forma matemática, el principio lógico transfiere la veracidad de la propiedad a lo largo de todo el espectro infinito del conjunto numérico ordenado.

---

## 4. Recursión y su Sinergia Computacional

La recursión es el reflejo computacional y algorítmico de la inducción matemática. Un objeto, estructura de datos o función se define recursivamente cuando se especifica en términos de instancias más simples de sí mismo.

Para que un proceso recursivo sea arquitectónicamente estable y no provoque un desbordamiento de memoria o bucle infinito en la pila de ejecución, debe incorporar dos elementos de diseño:

* **Caso Base (Condición de Parada):** El escenario más simple y elemental del problema, el cual se resuelve de manera directa sin necesidad de realizar nuevas invocaciones a la función.
* **Paso Recursivo:** La Unicode-descomposición del problema original mediante una auto-invocación que opera sobre un argumento reducido, asegurando una convergencia matemática progresiva hacia la condición de parada.

Por ejemplo, en el cálculo del factorial de un número entero ($n!$), el paso recursivo define el cálculo como $n \times (n - 1)!$, reduciendo continuamente el argumento hasta alcanzar el caso base definido de forma estricta para $0! = 1$.

---

## Ejercicios Prácticos y Algoritmos de Resolución

### Ejercicio 1: Validación Lógica de Integridad de Datos (Cuantificadores)

**Enunciado:** En un ecosistema distribuido de microservicios, se audita un conjunto de transacciones financieras $T$. Cada transacción $t$ cuenta con los atributos $\text{monto}(t)$ y $\text{autenticacion}(t)$, este último clasificado en $\text{\{"MFA", "Básica", "Ninguna"\}} $. Se requiere formalizar e implementar la siguiente regla de control de riesgos: *"Cualquier transacción con un monto superior a $50,000 debe procesarse obligatoriamente bajo autenticación MFA, y debe existir al menos una transacción registrada en el lote analizado"*.

**Formalización Lógica:**
$$\left( \forall t \in T \, (\text{monto}(t) > 50000 \rightarrow \text{autenticacion}(t) = \text{"MFA"}) \right) \land (\exists t \in T)$$

**Algoritmo de Resolución en Python:**
```python
def verificar_regla_transacciones(lote_transacciones):
    # Caso base implícito: verificar existencia de registros
    if not lote_transacciones:
        return False
        
    regla_universal_cumplida = True
    
    for t in lote_transacciones:
        # Evaluación de la implicación lógica del cuantificador universal
        if t['monto'] > 50000:
            if t['autenticacion'] != "MFA":
                regla_universal_cumplida = False
                break # Interrupción por detección de contraejemplo
                
    return regla_universal_cumplida

```

### Ejercicio 2: Demostración Formal Aplicada al Análisis Algorítmico (Inducción)

**Enunciado:** Demuestre por inducción matemática que la sumatoria de las potencias de base 2 para los primeros $n$ términos (desde 0 hasta $n-1$) cumple con la ecuación de asignación de memoria $2^n - 1$, lo cual fundamenta el límite de direccionamiento en arquitecturas de datos binarias:

$$1 + 2 + 4 + 8 + \dots + 2^{n-1} = 2^n - 1$$

**Resolución Paso a Paso:**

1. **Caso Base ($n = 1$):** Evaluamos el primer miembro del operador de suma, obteniendo $2^0 = 1$. Evaluamos el miembro derecho de la ecuación: $2^1 - 1 = 1$. La igualdad se verifica.
2. **Hipótesis Inductiva ($n = k$):** Asumimos la veracidad de la proposición para un valor arbitrario $k$:

$$1 + 2 + 4 + \dots + 2^{k-1} = 2^k - 1$$


3. **Paso Inductivo ($n = k + 1$):** Debemos probar que la estructura se mantiene para el término consecuente $k + 1$, es decir:

$$1 + 2 + 4 + \dots + 2^{k-1} + 2^{(k+1)-1} = 2^{k+1} - 1$$



Sustituyendo los primeros $k$ términos por su equivalencia directa dada en nuestra hipótesis inductiva, reducimos el miembro izquierdo:


$$(2^k - 1) + 2^k$$

Agrupamos los términos semejantes mediante factorización elemental:


$$2 \times 2^k - 1 = 2^{k+1} - 1$$

La igualdad es matemáticamente idéntica a la tesis planteada. Por consiguiente, bajo el principio de inducción matemática, queda demostrado que la ecuación es válida para todo de manera universal.

### Ejercicio 3: Recorrido de Estructuras Arbóreas Complejas (Recursión)

**Enunciado:** En las arquitecturas Big Data, las jerarquías organizacionales o taxonomías de datos estructurados se representan mediante grafos acíclicos dirigidos o árboles. Desarrolle un algoritmo recursivo capaz de computar la profundidad máxima (altura) de un árbol general para prevenir desbordamientos de pila (*stack overflow*) previos al parseo del volumen de información.

**Algoritmo de Resolución en Python:**

```python
class NodoEstructura:
    def __init__(self, identificador):
        self.id = identificador
        self.hijos = [] # Almacena referencias a subnodos jerárquicos

def calcular_profundidad_maxima(nodo_actual):
    # Caso Base: Si el nodo inspeccionado no posee ramificaciones
    if not nodo_actual.hijos:
        return 1
        
    # Paso Recursivo: Invocar recursivamente el cálculo sobre cada hijo
    profundidades = []
    for hijo in nodo_actual.hijos:
        profundidades.append(calcular_profundidad_maxima(hijo))
        
    # La profundidad del nodo es 1 más el máximo valor obtenido en sus ramas
    return max(profundidades) + 1

```

---

### Referencias Bibliográficas

[1. Morales & Díaz (2008). *Un estudio del concepto de variable en los libros de texto*. pp. 201-211.](https://www.researchgate.net/publication/268217377_UN_ESTUDIO_DEL_CONCEPTO_DE_VARIABLE_EN_LOS_LIBROS_DE_TEXTO)

[2. Usiskin, Z. (1988). *Conceptions of school algebra and uses of variables*. pp. 8-19.](https://es.scribd.com/document/358124587/Usiskin-Conceptions-of-school-algebra-and-uses-of-variables-pdf)

[3. Juárez, J. A. (2011). *Dificultades en la interpretación del concepto de variable en profesores de matemáticas de secundaria: un análisis mediante el modelo 3UV*. Números, 76, pp. 83-103.](https://es.scribd.com/document/161036447/Variables-Matematicas)

[4. Rosen, Kenneth H. (2019). *Matemática discreta y sus aplicaciones*. McGraw-Hill.](https://es.scribd.com/document/413993612/Mates-Discretas-Rosen-pdf)
