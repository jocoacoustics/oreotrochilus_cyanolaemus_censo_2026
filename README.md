# Formulación estadística y ecológica para la estimación censal corregida por detectabilidad de *Oreotrochilus cyanolaemus*

## 1. Marco del problema

El objetivo del análisis no es estimar directamente la población regional total de *Oreotrochilus cyanolaemus*, ni extrapolar densidad hacia todo el hábitat potencial. El objetivo es más específico y defendible: estimar la abundancia censal corregida por detectabilidad dentro del marco cubierto por el censo 2026.

El censo produce un conteo observado de individuos, denotado por $n_{obs}$. Sin embargo, en especies raras, móviles y de alta montaña, el conteo observado no puede interpretarse automáticamente como la abundancia real dentro del marco censal. No detectar un individuo durante una visita no implica que el individuo no exista ni que el sitio no esté siendo usado. Por ello se separan dos cantidades conceptualmente distintas: la abundancia censal subyacente y el proceso imperfecto de observación.

Denotamos por $N_C$ la abundancia censal subyacente, es decir, el número de individuos disponibles dentro del marco espacial y temporal cubierto por el censo 2026. Esta cantidad no se observa directamente. El censo observa solo una fracción de esos individuos, determinada por la probabilidad de detección. Denotamos esa probabilidad por $p_{det}$.

La estructura general del análisis es entonces:

$$
\text{censo 2026}\Rightarrow n_{obs},
$$

$$
\text{monitoreo repetido}\Rightarrow \widehat p_{det},
$$

$$
\widehat N_C=\frac{n_{obs}}{\widehat p_{det}}.
$$


Para los datos disponibles tenemos los siguientes resultados:

$$
n_{obs}=32,\quad
\widehat p_{crudo}=\frac{244}{964}=0.253,\quad
\widehat N_C=\frac{32}{0.253}\approx 126.4.
$$

También se reportan 278 puntos censales efectivos a 30 m, 69 sitios de monitoreo a 30 m, 244 visitas con detección y 964 visitas elegibles para el estimador crudo principal.

El censo aporta el conteo observado. El monitoreo repetido aporta información sobre detectabilidad. Esta separación es fundamental: el monitoreo repetido no se usa como conteo de abundancia principal porque sus visitas repetidas pueden generar pseudorreplicación temporal; en cambio, sí es útil para estimar con qué frecuencia la especie vuelve a ser detectada cuando se visitan sitios con evidencia de uso.



## 2. Población censal finita y proceso de observación

Sea

$$
\mathcal U_C=\{1,2,\ldots,N_C\}
$$

la población censal finita de individuos de *Oreotrochilus cyanolaemus* disponibles dentro del marco cubierto por el censo 2026. El tamaño de este conjunto es:

$$
|\mathcal U_C|=N_C.
$$

La cantidad $N_C$ representa la abundancia censal subyacente. No es directamente observable. Para cada individuo $k\in\mathcal U_C$, definimos una variable aleatoria de detección:

$$
Z_k=
\begin{cases}
1, & \text{si el individuo } k \text{ es detectado durante el censo},\\
0, & \text{si el individuo } k \text{ no es detectado durante el censo}.
\end{cases}
$$

El conteo observado durante el censo se define como la suma de estas detecciones individuales:

$$
n_{obs}=\sum_{k=1}^{N_C}Z_k.
$$

Esta ecuación es la base del modelo. Antes de hablar de una distribución binomial, se reconoce que el conteo censal observado es una suma de eventos individuales de detección/no detección.



## 3. Hipótesis que conducen al modelo binomial

Para que el conteo observado pueda modelarse mediante una distribución binomial, se requieren varias hipótesis. Estas hipótesis no deben ocultarse; deben declararse, auditarse cuando sea posible y matizarse cuando los datos no permitan verificarlas completamente.

Primero, se asume un marco censal operativamente cerrado durante el periodo corto del censo. Esto significa que, durante los días de muestreo, la población censal disponible se considera aproximadamente fija. No se está afirmando un cierre biológico perfecto, sino un cierre operativo razonable: en el intervalo de pocos días del censo, se supone que nacimientos, muertes, colonización o abandono del marco censal no alteran sustancialmente la cantidad $N_C$.

Segundo, se asume que cada individuo disponible tiene una respuesta observacional binaria: durante el censo, el individuo es detectado o no detectado. Esta es la razón de definir variables $Z_k$ con valores 0 y 1.

Tercero, se asume una probabilidad de detección común o promedio, denotada por $p_{det}$. En el modelo binomial puro, todos los individuos tienen la misma probabilidad de detección. En la realidad, la detectabilidad puede variar por sitio, hora, observador, clima, actividad de la especie, disponibilidad floral, comportamiento territorial o condiciones del paisaje. Por ello, $p_{det}$ debe interpretarse como una detectabilidad promedio efectiva del proceso de observación, estimada empíricamente mediante monitoreo repetido.

Cuarto, se asume independencia o independencia aproximada entre las detecciones individuales. Es decir, detectar un individuo no debería determinar de manera fuerte la detección de otro. Esta hipótesis puede verse afectada si hay grupos, parejas, territorios cercanos, puntos repetidos o doble conteo. Por esa razón, el diseño censal debe auditarse: número de días, puntos únicos, puntos repetidos, coordenadas repetidas y posibles duplicados. Si los puntos del censo fueron mayoritariamente únicos o se repitieron mínimamente, esto ayuda a defender la independencia operativa del conteo observado.

Bajo estas condiciones, para cada individuo $k$:

$$
Z_k\sim Bernoulli(p_{det}).
$$

Si además las variables $Z_1,\ldots,Z_{N_C}$ son independientes o aproximadamente independientes, entonces la suma de variables Bernoulli con la misma probabilidad de éxito sigue una distribución binomial:

$$
n_{obs}=\sum_{k=1}^{N_C}Z_k\sim Binomial(N_C,p_{det}).
$$

La distribución binomial tiene dos parámetros porque necesita especificar dos componentes del proceso de observación: el número de oportunidades de detección, $N_C$, y la probabilidad de éxito en cada oportunidad, $p_{det}$. En este contexto, el “éxito” es detectar a un individuo disponible.

Esta binomial no modela la dinámica ecológica completa de la especie. No modela nacimiento, muerte, colonización, ocupación, movimiento ni selección de hábitat. Modela únicamente el proceso de observación: de los individuos disponibles en el marco censal, cuántos fueron detectados.

Más formalmente, puede escribirse:

$$
n_{obs}\mid N_C,p_{det}\sim Binomial(N_C,p_{det}),
$$

donde la barra vertical indica que, si se fijaran hipotéticamente $N_C$ y $p_{det}$, el azar restante corresponde al número de individuos efectivamente detectados. Sin embargo, para lectura general puede escribirse simplemente:

$$
n_{obs}\sim Binomial(N_C,p_{det}),
$$

siempre que antes se haya explicado que $N_C$ y $p_{det}$ son los parámetros del modelo de observación.



## 4. Esperanza del conteo observado

Una propiedad básica de la distribución binomial es que, si

$$
n_{obs}\sim Binomial(N_C,p_{det}),
$$

entonces su esperanza es:

$$
E(n_{obs})=N_Cp_{det}.
$$

Esta expresión tiene una interpretación ecológica directa. Si dentro del marco censal hay $N_C$ individuos, pero cada uno se detecta con probabilidad $p_{det}$, entonces el conteo esperado no es $N_C$, sino solo la fracción detectable:

$$
\text{conteo esperado}=\text{abundancia censal}\times\text{detectabilidad}.
$$

Por tanto, si la detectabilidad es menor que 1, el conteo observado tenderá a ser menor que la abundancia censal real.

En el caso del censo 2026, el conteo observado es:

$$
n_{obs}=32.
$$

Ese valor debe interpretarse como abundancia mínima observada dentro del marco censal, no como abundancia censal corregida. Si la detección fuera perfecta, es decir, si $p_{det}=1$, entonces $n_{obs}=N_C$. Pero si $p_{det}<1$, entonces se espera que:

$$
n_{obs}\approx N_Cp_{det}.
$$

Despejando la abundancia censal:

$$
N_C\approx \frac{n_{obs}}{p_{det}}.
$$

Esta relación justifica el estimador de abundancia corregida por detectabilidad.



## 5. Estimador de abundancia corregida con detectabilidad conocida

Si $p_{det}$ fuera conocido, un estimador natural de la abundancia censal sería:

$$
\widehat N_C=\frac{n_{obs}}{p_{det}}.
$$

Bajo el modelo binomial, este estimador es insesgado cuando $p_{det}$ es conocido. En efecto:

$$
E(n_{obs})=N_Cp_{det}.
$$

Por lo tanto:

$$
E\left(\frac{n_{obs}}{p_{det}}\right)
=
\frac{E(n_{obs})}{p_{det}}
=
\frac{N_Cp_{det}}{p_{det}}
=
N_C.
$$

Así,

$$
E\left(\frac{n_{obs}}{p_{det}}\right)=N_C.
$$

Esto significa que, bajo las hipótesis del modelo y con detectabilidad conocida, la corrección $n_{obs}/p_{det}$ recupera en esperanza la abundancia censal subyacente.

Esta afirmación es importante, pero debe leerse con cuidado. El resultado de insesgadez corresponde al caso ideal en el cual $p_{det}$ es conocido. En la aplicación real, $p_{det}$ no se conoce y debe estimarse desde datos de monitoreo repetido. Por ello, la versión aplicada del estimador es:

$$
\widehat N_C=\frac{n_{obs}}{\widehat p_{det}}.
$$

Esta versión incorpora incertidumbre adicional y posibles sesgos asociados a la estimación de la detectabilidad.





## 5.1. Construcción del estimador por método de momentos

El estimador de abundancia censal corregida también puede construirse directamente mediante el método de momentos. Esta derivación muestra que la corrección no se introduce como una regla arbitraria, sino como consecuencia de igualar el momento observado del conteo con el momento esperado bajo el modelo de observación.

Sea $X=n_{obs}$ el conteo observado durante el censo. Supóngase que, condicionando en la abundancia censal $N_C$ y en la detectabilidad $p_{det}$, se cumple:

$$
X\mid N_C,p_{det}\sim Binomial(N_C,p_{det}).
$$

Bajo este modelo, el primer momento es:

$$
E(X\mid N_C,p_{det})=N_Cp_{det}.
$$

El método de momentos iguala el momento observado con el momento esperado. Por tanto:

$$
n_{obs}=N_Cp_{det}.
$$

Al despejar $N_C$, se obtiene:

$$
N_C=\frac{n_{obs}}{p_{det}}.
$$

Como $p_{det}$ no se conoce, se estima independientemente desde el monitoreo repetido. Si $Y$ es el número de visitas con detección y $M$ el número de visitas elegibles, entonces:

$$
Y\mid M,p_{det}\sim Binomial(M,p_{det}).
$$

y

$$
E(Y\mid M,p_{det})=Mp_{det}.
$$

Aplicando nuevamente el método de momentos:

$$
Y=Mp_{det},
$$

de donde:

$$
\widehat p_{det}=\frac{Y}{M}.
$$

Por tanto, el estimador aplicado de abundancia censal corregida es:

$$
\widehat N_C
=
\frac{n_{obs}}{\widehat p_{det}}
=
\frac{n_{obs}}{Y/M}
=
\frac{n_{obs}M}{Y}.
$$

En esta corrida, usando el estimador crudo principal de detectabilidad, la sustitución numérica es:

$$
\widehat N_C
=
\frac{32}{0.253}
\approx 126.4.
$$

Este estimador se interpreta como una corrección del conteo censal observado por la detectabilidad estimada desde monitoreo repetido. Su validez depende de que $\widehat p_{det}$ sea representativo de la detectabilidad efectiva durante el censo y de que el modelo binomial sea una aproximación razonable del proceso de observación.


## 6. Varianza del estimador con detectabilidad conocida

Si $p_{det}$ fuera conocido, la varianza del conteo observado bajo el modelo binomial es:

$$
Var(n_{obs})=N_Cp_{det}(1-p_{det}).
$$

Como el estimador ideal es:

$$
\widehat N_C=\frac{n_{obs}}{p_{det}},
$$

su varianza, condicionada a $p_{det}$ conocido, es:

$$
Var(\widehat N_C)
=
Var\left(\frac{n_{obs}}{p_{det}}\right).
$$

Como $p_{det}$ es una constante en este caso:

$$
Var\left(\frac{n_{obs}}{p_{det}}\right)
=
\frac{1}{p_{det}^2}Var(n_{obs}).
$$

Sustituyendo la varianza binomial:

$$
Var(\widehat N_C)
=
\frac{1}{p_{det}^2}N_Cp_{det}(1-p_{det}).
$$

Simplificando:

$$
Var(\widehat N_C)
=
\frac{N_C(1-p_{det})}{p_{det}}.
$$

Esta expresión muestra que la incertidumbre aumenta cuando la detectabilidad disminuye. Si $p_{det}$ es bajo, un mismo conteo observado puede ser compatible con una gama más amplia de abundancias censales.

En la práctica, como $N_C$ y $p_{det}$ no son conocidos, puede usarse una aproximación plug-in:

$$
\widehat{Var}(\widehat N_C)
=
\frac{\widehat N_C(1-\widehat p_{det})}{\widehat p_{det}}.
$$

Esta varianza describe la variabilidad asociada al conteo observado bajo detectabilidad conocida o reemplazada por su estimación. No agota toda la incertidumbre, porque $\widehat p_{det}$ también fue estimado. Por eso deben incluirse métodos adicionales, como delta/log-delta, inversión de intervalos y bootstrap por sitio.



## 7. Estimación de la detectabilidad desde monitoreo repetido

El censo aporta $n_{obs}$, pero no permite por sí solo estimar de manera robusta $p_{det}$. Para estimar detectabilidad se usa el monitoreo repetido. La lógica ecológica es que, en sitios donde la especie fue confirmada al menos una vez, las visitas repetidas permiten observar alternancia entre detecciones y no detecciones. Esa alternancia contiene información sobre la probabilidad de detectar la especie durante una visita.

Para cada sitio de monitoreo $i$ y visita $j$, definimos:

$$
Y_{ij}=
\begin{cases}
1, & \text{si se detecta } Oreotrochilus\ cyanolaemus \text{ en la visita }j\text{ al sitio }i,\\
0, & \text{si no se detecta}.
\end{cases}
$$

Sea $K_i$ el número de visitas realizadas al sitio $i$. Definimos el conjunto de sitios confirmados al menos una vez como:

$$
S^+=\{i:\exists j \text{ tal que } Y_{ij}=1\}.
$$

Es decir, $S^+$ contiene los sitios donde la especie fue detectada al menos una vez durante el monitoreo. En esos sitios, las visitas sin detección son informativas, porque ocurren en lugares donde la especie tiene evidencia de uso.

El estimador crudo global de detectabilidad se define como:

$$
\widehat p_{crudo}
=
\frac{\sum_{i\in S^+}\sum_{j=1}^{K_i}Y_{ij}}
{\sum_{i\in S^+}K_i}.
$$

En palabras, este estimador es:

> el total de visitas con *Oreotrochilus cyanolaemus* dividido para el total de visitas realizadas en sitios donde la especie fue confirmada al menos una vez.

Si definimos:

$$
X=\sum_{i\in S^+}\sum_{j=1}^{K_i}Y_{ij},
$$

como el número de visitas con detección, y

$$
M=\sum_{i\in S^+}K_i,
$$

como el número de visitas elegibles, entonces:

$$
\widehat p_{crudo}=\frac{X}{M}.
$$

Bajo un modelo binomial simple para las visitas elegibles:

$$
X\sim Binomial(M,p_{det}).
$$

En este caso:

$$
E(\widehat p_{crudo})=p_{det},
$$

y

$$
Var(\widehat p_{crudo})=\frac{p_{det}(1-p_{det})}{M}.
$$

Además, $\widehat p_{crudo}=X/M$ es el estimador de máxima verosimilitud de $p_{det}$ bajo el modelo binomial para visitas elegibles.

Este modelo para $\widehat p_{crudo}$ debe interpretarse como una aproximación. Las visitas repetidas dentro de un mismo sitio pueden estar correlacionadas, y la detectabilidad puede variar entre sitios. Por esa razón, además del intervalo binomial, se debe usar bootstrap por sitio y se debe mostrar la distribución empírica de detectabilidad por sitio.



## 8. Detectabilidad por sitio y heterogeneidad espacial

Para cada sitio confirmado $i$, se puede calcular una detectabilidad empírica por sitio:

$$
\widehat p_i=\frac{\sum_{j=1}^{K_i}Y_{ij}}{K_i}.
$$

Esta cantidad representa la proporción de visitas al sitio $i$ en las que se detectó la especie. No se usa como estimador principal de abundancia porque puede ser inestable cuando $K_i$ es pequeño. Por ejemplo, un sitio con una visita y una detección tendría $\widehat p_i=1$, pero eso no implica detectabilidad perfecta. Sin embargo, $\widehat p_i$ es muy útil como diagnóstico espacial y ecológico.

La distribución de los valores $\widehat p_i$ permite evaluar si la detectabilidad es relativamente homogénea entre sitios o si hay sitios con detectabilidad muy alta y otros con detectabilidad baja. Si existe mucha heterogeneidad, el estimador global $\widehat p_{crudo}$ debe interpretarse como una detectabilidad promedio efectiva.

Por ello, el análisis debe incluir:

$$
\{\widehat p_i:i\in S^+\},
$$

su distribución empírica, el número de visitas por sitio $K_i$, y un mapa de detectabilidad por sitio. En el mapa, la burbuja puede representar el sitio, el color puede representar $\widehat p_i$, el tamaño puede representar $K_i$ o el número de visitas con detección, y la etiqueta visible puede mostrar $\widehat p_i$ redondeado o el cociente detecciones/visitas.



## 9. Estimadores alternativos de detectabilidad

El estimador crudo global se usa como estimador principal porque conserva información en una especie rara. Sin embargo, es importante evaluar sensibilidad mediante estimadores alternativos.

### 9.1. Detectabilidad del periodo comparable al censo

Sea $T_C$ el conjunto de visitas realizadas en el periodo comparable al censo, por ejemplo el mismo mes calendario. El estimador del periodo comparable es:

$$
\widehat p_{periodo}
=
\frac{\sum_{i\in S^+}\sum_{j\in T_C}Y_{ij}}
{\sum_{i\in S^+}\sum_{j\in T_C}1}.
$$

Este estimador responde si la detectabilidad durante el periodo comparable al censo fue mayor o menor que la detectabilidad promedio. No necesariamente se usa como estimador principal porque puede tener menor tamaño muestral y puede mezclar años distintos, pero es una sensibilidad temporal importante.

### 9.2. Estimador leave-one-out

El estimador crudo usa sitios confirmados al menos una vez. Eso puede generar una forma de circularidad: una visita puede contribuir a confirmar el sitio y también a estimar detectabilidad. Para evaluar esa posible circularidad, se define un estimador leave-one-out.

Para cada visita $j$ del sitio $i$, definimos:

$$
S_{ij}^{+,-j}=
\begin{cases}
1, & \text{si existe una visita } k\ne j \text{ al mismo sitio con }Y_{ik}=1,\\
0, & \text{en otro caso}.
\end{cases}
$$

Entonces:

$$
\widehat p_{LOO}
=
\frac{\sum_i\sum_jY_{ij}S_{ij}^{+,-j}}
{\sum_i\sum_jS_{ij}^{+,-j}}.
$$

Este estimador solo considera una visita como elegible si el sitio fue confirmado por otra visita distinta. Reduce circularidad, pero puede descartar información valiosa de sitios con pocas visitas o detecciones únicas. Por eso debe usarse como comparación técnica, no necesariamente como estimador principal.



## 10. Detectabilidad temporal

La detectabilidad puede variar en el tiempo. Para evaluar esa variación, se agrupan las visitas por periodo $t$, que puede ser mes, bimestre u otra unidad temporal coherente con el monitoreo.

Para cada periodo $t$, definimos:

$$
X_t=\sum_{i\in S^+}\sum_{j\in t}Y_{ij},
$$

como el número de visitas con detección en ese periodo, y

$$
M_t=\sum_{i\in S^+}\sum_{j\in t}1,
$$

como el número de visitas elegibles en ese periodo.

La detectabilidad temporal estimada es:

$$
\widehat p_t=\frac{X_t}{M_t}.
$$

Bajo un modelo binomial por periodo:

$$
X_t\sim Binomial(M_t,p_t),
$$

donde $p_t$ es la detectabilidad promedio durante el periodo $t$. Esta serie no reemplaza el estimador global; funciona como diagnóstico. Si la detectabilidad varía fuertemente entre periodos, entonces el estimador global debe interpretarse como una corrección promedio, y el periodo comparable al censo adquiere mayor importancia como análisis de sensibilidad.



## 11. Abundancia corregida por detectabilidad estimada

Como $p_{det}$ no se conoce, se reemplaza por una estimación obtenida desde el monitoreo repetido. El estimador aplicado es:

$$
\widehat N_C=\frac{n_{obs}}{\widehat p_{det}}.
$$

Cuando se usa el estimador crudo global:

$$
\widehat N_{C,crudo}
=
\frac{n_{obs}}{\widehat p_{crudo}}.
$$

Cuando se usa el estimador del periodo comparable:

$$
\widehat N_{C,periodo}
=
\frac{n_{obs}}{\widehat p_{periodo}}.
$$

Cuando se usa leave-one-out:

$$
\widehat N_{C,LOO}
=
\frac{n_{obs}}{\widehat p_{LOO}}.
$$

Estos tres valores no deben leerse como tres poblaciones distintas, sino como una evaluación de sensibilidad ante distintas formas de estimar la detectabilidad.

El resultado principal debe ser la abundancia censal corregida por detectabilidad bajo el estimador principal de detectabilidad, acompañada de intervalos y sensibilidad. El conteo observado $n_{obs}$ debe reportarse siempre como abundancia mínima observada.



## 12. Incertidumbre mediante aproximación delta y escala logarítmica

La incertidumbre de $\widehat N_C=n_{obs}/\widehat p_{det}$ proviene de dos fuentes: la variabilidad del conteo observado y la incertidumbre en la estimación de la detectabilidad.

Una forma natural de trabajar es usar la escala logarítmica:

$$
\log(\widehat N_C)=\log(n_{obs})-\log(\widehat p_{det}).
$$

La escala logarítmica es útil porque la abundancia corregida es positiva y porque los errores relativos son más interpretables que los errores absolutos.

Una aproximación delta para el error estándar de $\log(\widehat N_C)$ puede escribirse como:

$$
SE_{\log(\widehat N_C)}
\approx
\sqrt{
Var(\log(n_{obs}))
+
Var(\log(\widehat p_{det}))
}.
$$

Bajo aproximaciones binomiales, una forma práctica es:

$$
SE_{\log(\widehat N_C)}
\approx
\sqrt{
\frac{1-\widehat p_{det}}{n_{obs}}
+
\frac{1-\widehat p_{det}}{M\widehat p_{det}}
}.
$$

El primer término aproxima la incertidumbre del conteo observado; el segundo aproxima la incertidumbre de la detectabilidad estimada desde $M$ visitas elegibles.

Luego, un intervalo aproximado al 95% en escala original es:

$$
IC_{95\%}
=
\left[
\widehat N_C\exp(-1.96SE_{\log}),
\;
\widehat N_C\exp(1.96SE_{\log})
\right].
$$

Este intervalo evita límites negativos y expresa incertidumbre multiplicativa, coherente con la forma del estimador $n_{obs}/\widehat p_{det}$.



## 13. Intervalo por inversión del intervalo de detectabilidad

Otra forma transparente de propagar la incertidumbre es invertir directamente el intervalo de confianza de la detectabilidad.

Si el intervalo de confianza para $p_{det}$ es:

$$
IC(p_{det})=[p_{inf},p_{sup}],
$$

entonces, como la función

$$
N(p)=\frac{n_{obs}}{p}
$$

es decreciente en $p$, el intervalo de abundancia se invierte:

$$
IC(N_C)=
\left[
\frac{n_{obs}}{p_{sup}},
\frac{n_{obs}}{p_{inf}}
\right].
$$

La interpretación es directa. Si la detectabilidad real fuera menor, el mismo conteo observado representaría más individuos. Si la detectabilidad real fuera mayor, el mismo conteo representaría menos individuos.

Este intervalo es especialmente útil en comunicación porque muestra de manera clara cómo la incertidumbre en $p_{det}$ se traduce en incertidumbre en $N_C$.



## 14. Bootstrap por sitio

Las visitas dentro de un mismo sitio no son necesariamente independientes. Un sitio puede tener condiciones particulares que aumentan o reducen la detectabilidad. Por eso, además de intervalos binomiales, se usa bootstrap por sitio.

Sea $S^+$ el conjunto de sitios confirmados. En cada iteración bootstrap $b$, se remuestrean sitios completos con reemplazo:

$$
S^{(b)}=\{i_1^{(b)},i_2^{(b)},\ldots,i_m^{(b)}\}.
$$

Para ese remuestreo se recalculan las detecciones y visitas elegibles:

$$
X^{(b)}
=
\sum_{i\in S^{(b)}}\sum_jY_{ij},
$$

$$
M^{(b)}
=
\sum_{i\in S^{(b)}}K_i.
$$

Luego:

$$
\widehat p^{(b)}=\frac{X^{(b)}}{M^{(b)}},
$$

y

$$
\widehat N^{(b)}=\frac{n_{obs}}{\widehat p^{(b)}}.
$$

La distribución de los valores $\widehat N^{(b)}$ representa la incertidumbre asociada a la heterogeneidad entre sitios. Un intervalo bootstrap al 95% puede obtenerse con percentiles:

$$
IC_{boot,95\%}
=
\left[
Q_{0.025}(\widehat N^{(b)}),
Q_{0.975}(\widehat N^{(b)})
\right].
$$

Este procedimiento no resuelve todos los problemas de dependencia, pero es más coherente que remuestrear visitas sueltas cuando las visitas están agrupadas por sitio.



## 15. Sesgo por estimar la detectabilidad

La insesgadez exacta de $n_{obs}/p_{det}$ se cumple cuando $p_{det}$ es conocido. En la práctica usamos:

$$
\widehat N_C=\frac{n_{obs}}{\widehat p_{det}}.
$$

Aunque $\widehat p_{det}$ fuera insesgado para $p_{det}$, la transformación $1/x$ es convexa. Por la desigualdad de Jensen:

$$
E\left(\frac{1}{\widehat p_{det}}\right)
\geq
\frac{1}{E(\widehat p_{det})}.
$$

Por tanto, la variabilidad de $\widehat p_{det}$ puede introducir sesgo positivo en la abundancia corregida. Es decir, la incertidumbre en la detectabilidad tiende a inflar la esperanza de $1/\widehat p_{det}$.

Sin embargo, existe una tensión en sentido contrario. Si el monitoreo repetido sobreestima la detectabilidad real del censo, entonces la abundancia corregida puede quedar subestimada. Sea $p_C$ la detectabilidad real durante el censo y $\widehat p_{mon}$ la detectabilidad estimada desde monitoreo. Si:

$$
\widehat p_{mon}>p_C,
$$

entonces:

$$
\frac{n_{obs}}{\widehat p_{mon}}
<
\frac{n_{obs}}{p_C}.
$$

Esto significa que, si la detectabilidad estimada desde monitoreo es mayor que la detectabilidad efectiva del censo, la corrección produce una abundancia menor que la que se obtendría usando la detectabilidad censal real.

Por esta razón, el resultado no debe presentarse como un número absoluto cerrado. Debe presentarse como una estimación censal corregida por detectabilidad, acompañada de intervalos, bootstrap, estimadores alternativos y discusión explícita de sesgos.



## 16. Diagnóstico empírico de las hipótesis binomiales

La formulación binomial requiere hipótesis. Algunas son conceptuales y otras pueden auditarse empíricamente.

Para evaluar cierre operativo, se debe reportar el periodo exacto del censo, el número de días muestreados y la distribución de visitas por día. Un censo concentrado en pocos días fortalece la interpretación de población censal aproximadamente fija.

Para evaluar independencia operativa y riesgo de doble conteo, se debe reportar:

$$
\text{número de puntos únicos},
$$

$$
\text{número de puntos repetidos},
$$

$$
\text{máximo número de visitas por punto},
$$

$$
\text{número de coordenadas repetidas},
$$

$$
\text{posibles duplicados por fecha, hora, punto, especie, sexo y distancia}.
$$

Si los puntos se repiten poco o nada, se puede argumentar que el diseño reduce la dependencia por reobservación del mismo individuo en el mismo lugar. Si hay repeticiones, deben auditarse y discutirse como posible fuente de dependencia o doble conteo.

Para evaluar la calidad del conteo, se debe separar claramente:

$$
\text{registros de especie primaria}
$$

de

$$
\text{registros en campos secundarios o de interacción}.
$$

El conteo censal principal debe basarse en la especie primaria del registro, no en campos secundarios que podrían representar interacciones, notas o registros auxiliares.

Para evaluar la detectabilidad, se debe reportar la estructura del monitoreo repetido: visitas por sitio, sitios confirmados, visitas elegibles, detecciones, distribución temporal y distribución de detectabilidad empírica por sitio.

Si las hipótesis binomiales no se cumplen estrictamente, el modelo debe declararse como una aproximación de primer orden. La defensa entonces descansa en tres elementos: auditoría de diseño, sensibilidad de estimadores y bootstrap por sitio.



## 17. Calidad de datos y reglas de limpieza

Dado que las bases provienen de archivos Excel de campo, se requiere una capa explícita de limpieza reproducible. Las decisiones de limpieza deben documentarse y no quedar ocultas en el código.

Las reglas mínimas son:

1. Para el censo, el conteo de individuos observados debe usar la columna primaria de especie. No deben mezclarse especies registradas en campos de interacción o notas como si fueran registros censales principales.

2. Para el monitoreo, la unidad de análisis de detectabilidad debe ser la visita agregada a sitio, no la fila bruta si varias filas pueden corresponder a un mismo evento, punto o visita.

3. Las coordenadas deben validarse y transformarse a formato numérico.

4. Las fechas deben convertirse a objetos de fecha válidos.

5. Los sitios o puntos deben construirse con reglas explícitas, usando los campos disponibles: lugar, ruta, punto, coordenadas u otros identificadores.

6. Las repeticiones deben distinguirse de duplicados. Una visita repetida puede ser válida para estimar detectabilidad; un duplicado accidental no debe inflar detecciones.

7. Toda tabla limpia debe conservar referencia a la fuente original.

8. Toda métrica del dashboard debe poder rastrearse a una tabla limpia, una regla de agregación y, si es posible, una consulta SQL reproducible.



## 18. Justificación de no usar Distance Sampling ni MaxEnt como estimador poblacional

Distance Sampling no se usa en esta versión porque requeriría un modelo explícito de detección en función de la distancia, supuestos de detección perfecta a distancia cero, mediciones confiables de distancia y un diseño apropiado para estimar densidad. Mezclar Distance Sampling con la corrección temporal de detectabilidad del monitoreo repetido introduciría otro proceso de detección y complicaría la interpretación.

MaxEnt tampoco se usa para estimar abundancia. MaxEnt puede aportar una referencia espacial de idoneidad o hábitat potencial, pero una capa de idoneidad no equivale a densidad ni a número de individuos. Por eso MaxEnt puede mostrarse como capa visual de contexto, preferiblemente liviana y transparente, pero no debe entrar en el cálculo de $N_C$.

El resultado principal sigue siendo:

$$
\widehat N_C=\frac{n_{obs}}{\widehat p_{det}},
$$

dentro del marco censal 2026.



## 19. Interpretación ecológica del resultado

El valor $n_{obs}=32$ debe reportarse como abundancia mínima observada durante el censo 2026. La abundancia corregida por detectabilidad estima cuántos individuos serían compatibles con ese conteo si se reconoce que la detección fue imperfecta.

Si se usa la detectabilidad principal estimada, 0.253, entonces la corrección tiene la forma:

$$
\widehat N_C\approx \frac{32}{0.253}\approx 126.4.
$$

El resultado no debe interpretarse como el número total de individuos de la especie en toda su distribución. Debe interpretarse como una abundancia censal corregida dentro del marco espacial y temporal evaluado.

La lectura final debe ser cautelosa:

> El censo observó directamente 32 registros primarios. Bajo una corrección por detectabilidad estimada desde monitoreo repetido, la abundancia censal compatible con ese conteo es mayor que el conteo observado. La magnitud de la corrección depende de la detectabilidad estimada y de sus supuestos. Por ello se reportan intervalos, sensibilidad temporal, leave-one-out, bootstrap por sitio y diagnóstico de calidad de datos.



## 20. Estructura conceptual final

La estructura metodológica completa puede resumirse así:

$$
\mathcal U_C=\{1,\ldots,N_C\}
$$

define la población censal subyacente.

$$
Z_k\in\{0,1\}
$$

define la detección individual durante el censo.

$$
n_{obs}=\sum_{k=1}^{N_C}Z_k
$$

define el conteo observado.

Bajo cierre operativo, detectabilidad promedio e independencia aproximada:

$$
Z_k\sim Bernoulli(p_{det})
$$

y

$$
n_{obs}\sim Binomial(N_C,p_{det}).
$$

La esperanza es:

$$
E(n_{obs})=N_Cp_{det}.
$$

Si $p_{det}$ fuera conocido:

$$
E\left(\frac{n_{obs}}{p_{det}}\right)=N_C.
$$

Como $p_{det}$ es desconocido, se estima desde monitoreo repetido:

$$
\widehat p_{crudo}
=
\frac{\text{visitas con detección en sitios confirmados}}
{\text{visitas elegibles en sitios confirmados}}.
$$

La abundancia censal corregida es:

$$
\widehat N_C=\frac{n_{obs}}{\widehat p_{det}}.
$$

La incertidumbre se evalúa mediante:

$$
IC_{\log-delta},
$$

$$
IC(N)=
\left[
\frac{n_{obs}}{p_{sup}},
\frac{n_{obs}}{p_{inf}}
\right],
$$

y bootstrap por sitio:

$$
\widehat N^{(b)}=\frac{n_{obs}}{\widehat p^{(b)}}.
$$

La sensibilidad se evalúa comparando:

$$
\widehat p_{crudo},
\quad
\widehat p_{periodo},
\quad
\widehat p_{LOO},
\quad
\widehat p_t,
\quad
\widehat p_i.
$$

Y la interpretación final queda limitada al marco censal:

> abundancia censal corregida por detectabilidad, no población regional total.
