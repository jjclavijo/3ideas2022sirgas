---
header-includes:
  - \setmainfont{Quicksand}
  - \setbeamercolor{frametitle}{fg=white}
  - \setbeamercolor{background canvas}{bg=black}
  - \setbeamercolor{normal text}{fg=white}
  - \setbeamercolor{frametitle}{fg=orange}
---

# Tres ideas en torno a la reproducibilidad de los procesamientos geodésicos.

### Javier José Clavijo
\small jclavijo@fi.uba.ar
\newline
\small https://github.com/jjclavijo/3ideas2022sirgas

### Universidad de Buenos Aires - Facultad de Ingeniería

---

## Motivación (origen)

- Posiciones, en un MR,
  $\longleftrightarrow$ $\underset{x}{\arg\max} P(X|\text{\footnotesize datos})$
  \footnote{\tiny \textit{Marcos de referencia geodésicos: un enfoque Bayesiano; JJ Clavijo, JF Martínez}, \\ en \guillemotleft Seminario de vinculación y transferencia: año 3\guillemotright \textbf{ISBN 978-987-88-4967-6} \url{https://cms.fi.uba.ar/uploads/Libro_SE_Vy_T_2021_VERSION_FINAL_add8815fd9.pdf}}

- Si resuelvo X por Pedazos (ej: órbitas $\rightarrow$ $X_0$)

- $P(X_1|\text{\footnotesize datos}) = P(X_1|\text{\footnotesize datos},X_0)$
  - $\mapsto$ condicionar a los parámetros fijos es igual a la marginalizar.
  - $\mapsto$ $X_1$ y $X_0$ son condicionalmente independientes a los datos.
  - No pasa si hay datos compartidos.

- $\mapsto$ Necesito saber si $P(X_0,\text{datos}) = P(X_0)P(\text{datos}) \forall  \text{modelos}$

- Y necesito sistematizarlo.

<!---

La principal motivación es que, dado a proponer aplicar métodos bayesianos a la materialización de los marcos de referencia es importante entender cuales son los priors, las correlaciones, etc.

Aquí topamos con algunas dificultades a la hora de analizar y comparar los procesamientos publicados.

Incluso se hace dificil decidir si determinado conjunto de datos publicado es apto para un objetivo concreto, porque no podemos saber si hay correlaciones no declaradas que nos puedan afectar el resultado si no sabemos cómo se relacionan con sus datos de entrada.

Es importante remarcar que se CONDICIONA cuando se eliminan columnas de ATPA y se MARGINALIZA cuando se eliminan columnas de SIGMA.

--->

---

## Motivación (origen)

Al analizar trabajos publicados aparece

- Software específico.
- Formas de leer y estructurar datos siempre nuevas.
- Nomenclatura especial.
- Términos y Métodos "heredados"

Puede dificultarse

- Aprender por asociación
- Reproducir experimentos
- Validar Resultados

---

## Lógica

### Premisas

- Formatos estándar de Intercambio $\in$ Geodesia
- Flujos de datos estandarizados $\notin$ Geodesia
- $\exists$ W3C PROV Standard
- $\exists$ Metodos Bayesianos - Redes Bayesianas, etc
- $\exists$ Métodos de validación, Herramientas genéricas de procesamiento y transmisión de datos

---

## Lógica

### Observando que

- Datos de Observacion $\mapsto$ Tensor Ralo o Columnar Format (índice: t).
- Modelos paramétricos $\mapsto$ Conjuntos de parámetros $\mapsto$ Tensor Denso o Columnar Format (índice: t).
- Resultados $\mapsto$ $\mu,\Sigma$ de una $\mathcal{N}$ (hoy).

---

## Lógica

### Podemos plantear

- Segmentación en función del tiempo (con Herramientas Genéricas)
- Validación por bloques (Hash)
- Flujos de trabajo "funcionales" (PROV, Reproducibilidad)
- Identificación y descripción de paramétros y dependencia. (PROV, Redes Bayes)

---

## Bajando a nuestro caso

---

## Datos de entrada

1. $\uparrow\uparrow$ Datos (observaciones $+$)
2. $\uparrow\uparrow$ Procesos
3. $\uparrow\uparrow$ Modelos
    1. $\uparrow\uparrow$ Parámetros \newline Provistos $\neq$ Datos $\rightarrow$ Optimización $\rightarrow$ Ajustados.

![Esquema "ideal"]()
![Esquema "real"]()

<!---

--->

---

## Algoritmos de inferencia

Los métodos que usamos para hallar "resultados", que son valores para los parámetros de un modelo, a partir de "datos".

1. Tienen Hiperparámetros.
2. Pueden variar entre implementaciones (por tener variantes).
3. Pueden tener "imprecisiones" que se deciden en cada implementación.

<!---

Ejemplo: Cuando estamos usando un filtro Kallman, mas allá de las multiples variantes de este, ¿qué significa "fijar" ambiguedades? ¿Se las ignora en el filtro o se fuerza el resultado?

--->

---

## Distribución de los datos

1. No es homogénea
2. Difícilmente permite validar con conjuntos independientes
3. Puede haber correlaciones ocultas a través de parámetros "dados por hecho".

---

# Tres ideas introduciendo

los conceptos de

1. Funcionalidad
1. Replicabilidad.
1. Reproducibilidad.
1. Robustez.
1. Validación.
1. Rastreo de origen. (data provenance)

<!---

Acá justificamos el título de la charla. Tenemos tres ideas para introducir estos conceptos, que nos parecen importantes para poder llevar ordenadamente el procesamiento geodésico a que sea mas accesible, enseñable y explorable.

La primera idea es buscar la forma de estandarizar o inventariar (no seamos pretenciosos) el registro de "qué procesos se siguieron hasta llegar a este producto". De esta manera podríamos generar un "registro de flujo de datos". Es importante que el registro sea sowtware independiente, asique hay que centrarse en "datos" + "algoritmos" + "hiperparámetros".

La segunda se refiere a un hecho más básico, que es que etenemos estándares para algunos tipos de datos en la forma de transmitirlos pero no en la forma de tratarlos. Para poder garantizar la replicabilidad necesitamos garantizar la identidad de los datos. Acá vamos a hablar de RINEX y SINEX como ejemplos, de hashes como herramienta de comparación rápida, de posibles "primeros pasos" para facilitar el trabajo con datos de observaciones (arrow, etc). Y de Sub-Setting de datos (respecto del SINEX). Con un Apartado sobre SINEX y Bayes.

La tercera idea es relativa al problema de la validación y a cómo informamos y usamos los productos IGS SIRGAS, etc. El planteo es poder analizar cual es el origen de estos productos, cómo pueden introducir correlaciones involuntarias, y qué alternativas podríamos plantear para evitarlo/mitigarlo.

--->

# Idea 1

## Aplicar el estándar PORV-O

Agente - Entidad - Acción

- Esquema funcional ($=$ entradas $\mapsto$ $=$ salidas)
- Red Bayesiana


<!---

Datos
Algoritmos
Hiperparámetros

Ejemplo: Leerse 150 paper para saber qué tipo de marco de referencia usan y qué tipo de modelo usan para ajustar saltos.

   o
-\_|_/-

https://www.w3.org/TR/2013/REC-prov-o-20130430/

Notar la relación entre Prov y Bayes networks.

http://videolectures.net/iswc2014_gil_semantic_challenges/ -> 18:00 ++

- Hanalyzer?

- Wings - Workflow (gil et al 2011 JETAI)

--->

---

## Aplicar el estándar PORV-O

Ejemplo: Analizar algoritmos de detección de discontinuidad

Leer 150 papers para saber

- ¿En qué MR trabajan? (como hiperparámetro al menos)
- ¿Qué tipo de modelo aplica? (Lineal?)
- ¿Hasta qué distancia "detectan"?

Ej de provecho: Modelos lineales no dependen de cambios lineales del MR

---

## Caso 1:

Coordenadas Nevada -> Modelo lineal

## Caso 2:

Coordenadas Sirgas -> "realineación" -> Modelo paramétrico

## Caso 3:

Procesamiento -> Alineado a Sirgas -> Modelo...

## Caso 4:

Mi Caso

---

# Idea 2

## Planteo

### El formato RINEX es texto $\mapsto$

- No define tipo de dato estandarizado para cada variable.
- Depende de un parser que puede ser mas o menos tolerante.
- Espacios y ceros pueden "cambiar" el archivo sin cambiar el dato.

### Datos transmitidos por NTRIP También son (otro) texto.

### BINEX

- Mejora todo esto, pero no es Columnar y los tipos de dato no
  son estándares de computadora (sigue habiendo algo de nicho)...

<!---

Esta idea es tener un control más rígido de los datos y una forma más compartida de usarlos. El ejemplo práctico es qué pasa cuando alguien pesca los datos del NTRIP si después baja un rinex del mismo dato. ¿cómo chequea es?
Además, cada software tiene formas lijeramente distintas de agrupar los datos, de forma que se hace dificil rastrear que están haciendo exactamente el mismo algoritmo.
Pensando nuevamente en los workflows de la idea 1, aplicar algo de columnar format o algo así suena una idea razonable.

Apendice: Volviendo a la s bayes networks, qué nos dicen los sinex de todo esto?.

Importante hablar de Parsers y Metadatos.

--->

---

## Planteo

La naturaleza del dato es Observaciones de una variedad de indicadores
indexados por el tiempo

- Se puede estandarizar en columnas con tipo de dato determinado

---

## Utilidades

- Al fijar el tipo de dato se puede comparar datos (no archivos) con hashes.
  -  (BINEX podría permitirlo, aunque mezcla muchos indicadores "extra")

- Se podría partir y transmitir los datos eficientemente. (aplicaciones RT) (y validarlos)

- Se puede usar entornos como spark, arrow-flight, etc.

---

## Hashes

https://github.com/jjclavijo/sirgas2022hashes

---

## Columnar Format: Flujos de trabajo

https://github.com/jjclavijo/sirgas2022arrow

---

# Idea 3

## Planteo

Es muy difícil garantizar la independencia real de procesamientos, aún si separáramos redes que no se conectan.

<!---

Construir sobre Productos podría no ser tan trivial como parece. Ejemplo: Orbitas surgen de procesamientos que resultan en posiciones y correlaciones de estaciones que DESPUES SE ASUMEN DESCORRELACIONADAS.

IGS con un SINEX MONSTRUOSO!

--->

---

# Idea 3

## Observación

Los productos publicados no describen su propio origen (condicional o marginal).

Ejemplo: Los SINEX pueden ser subsets de otros SINEX: condicionales ${X_1 = X|X_0}$ o marginales ${X_1 \ni P(X_1)\times P(X_0) \neq 0}$

Los sp3 dan parámetros ($\theta$) de órbitas pero no describen $P(\theta,x_0)$

Si nuestros parámetros ($X_2$) son tales que $X_0 \cap X_2 \neq \emptyset$
estamos perdiendo información, porque no sabemos nada de P(X_0).

---

## Observación

- El SINEX de SIRGAS no describe su dependencia del SINEX de óbitas de IGS,
  de hecho lo ignora porque usa los sp3 para calcular.
- Rastreando el origen de datos podría rastrearse esa dependencia (desde el SINEX de IGS)
- Esto permitiría diseñar la combinación de forma distinta usando una red bayesiana y Beleaf propagation

---

## Ejemplo

Dependencias SINEX bayes net. SIRGAS CODE IGS

---

## Validación total (?)

Una idea intereseante:

- Tener conjuntos de órbitas independientes.
- Validar procesamientos con verdadera independencia modelos / datos.

---

## ¡Muchas Gracias!
