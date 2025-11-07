# Estadística y Análisis de Datos — Spotify

Proyecto del módulo de Estadística y Análisis de Datos utilizando un dataset de Spotify.

El objetivo es realizar un Análisis Exploratorio de Datos (EDA) para comprender las características de las canciones dentro del dataset y detectar patrones relacionados con la popularidad, energía, bailabilidad, tempo, etc.

El dataset contiene más de 114,000 canciones con variables como popularidad, duración, energía, danceability, valence (felicidad), tempo, entre otras.

---

## Objetivos del proyecto

- Aplicar análisis exploratorio de datos (EDA)
- Usar estadísticas descriptivas
- Detectar valores atípicos (outliers)
- Visualizar relaciones entre variables
- Generar insights que permitan comprender el comportamiento de las canciones

---

## Tecnologías utilizadas

| Tecnología / Librería | Uso |
|----------------------|-----|
| Python | Lenguaje principal |
| Pandas | Manipulación y análisis de datos |
| NumPy | Estadística |
| Matplotlib / Seaborn | Visualización |
| VS Code + Jupyter Notebook | Desarrollo |

---

## Variables principales del dataset

| Variable | Significado |
|----------|-------------|
| `popularity` | Popularidad de la canción (0 a 100) |
| `danceability` | Qué tan bailable es una canción (0 = nada, 1 = muy bailable) |
| `energy` | Nivel de energía (0 = calma, 1 = muy energética) |
| `loudness` | Volumen promedio en decibelios |
| `acousticness` | Nivel de acústica de la canción |
| `instrumentalness` | Probabilidad de que una canción sea instrumental |
| `valence` | Qué tan “feliz/positiva” suena la canción |
| `tempo` | Velocidad en BPM (beats por minuto) |

---

## Análisis Estadístico (df.describe())

A partir de la estadística descriptiva se identificaron los siguientes insights:

| Variable | Insight relevante |
|----------|------------------|
| Popularity (popularidad) | La canción promedio tiene una popularidad de 33/100, pero algunas llegan a 100. La distribución está sesgada hacia valores bajos (pocas canciones son muy populares). |
| Duration_ms (duración) | Duración promedio aproximada de 3.8 minutos. Existen valores extremos (hasta 87 minutos), lo que indica outliers. |
| Danceability (bailable) | Media de 0.56, por lo que la mayoría de canciones son moderadamente bailables. |
| Energy (energía) | Media de 0.64, predominan canciones con alta energía. |
| Acousticness (acústica) | Media de 0.31, la mayoría no son acústicas (predominan producciones de estudio). |
| Instrumentalness | Mediana cercana a 0, casi ninguna canción es instrumental (la mayoría tiene voz). |
| Valence (felicidad) | Media de 0.47, hay equilibrio entre canciones felices y tristes. |
| Tempo (BPM) | Promedio cercano a 122 BPM, típico de géneros como pop o dance. |

Nota: En este módulo solo se identifican los outliers.  


---

## Visualizaciones generadas

1. **Histograma — Distribución de variables numéricas**  
   Muestra cuántas canciones se encuentran dentro de cada rango de valores.  
   Archivo generado: `/images/histograma_variables_numericas.png`

2. **Boxplot — Detección de outliers**  
   Permite visualizar valores extremos, especialmente en la duración (`duration_ms`).  
   Archivo generado: `/images/boxplot_outliers.png`

3. **Matriz de correlación**  
   Muestra relaciones entre variables numéricas.  
   Correlaciones relevantes:
   - `energy` y `loudness` tienen correlación alta (las canciones con más energía suelen ser más fuertes).
   - `danceability` y `popularity` tienen correlación baja (ser bailable no garantiza popularidad).  
   Archivo generado: `/images/matriz_correlacion.png`

---

## Conclusiones

- El análisis exploratorio del dataset de Spotify permitió identificar patrones relevantes sobre las características de las canciones y su relación con la popularidad:

- La distribución de la popularidad es desigual y está sesgada hacia valores bajos.
La popularidad promedio es 33/100, pero existen canciones que alcanzan 100. Esto indica que el catálogo de Spotify está dominado por canciones poco reproducidas, mientras que solo un pequeño porcentaje concentra la atención de los usuarios.

- La duración promedio de una canción es consistente con estándares comerciales (≈ 3.8 min), pero existen valores fuera de rango (hasta 87 min).
Estos outliers pueden corresponder a versiones extendidas, podcasts o errores de registro. Detectarlos es clave antes de cualquier modelado.

- Las canciones son principalmente energéticas y bailables.
Las variables danceability, energy y valence muestran que los valores se concentran en rangos medios–altos, lo cual es coherente con géneros comerciales contemporáneos como pop, EDM o reggaetón.

- La correlación confirma relaciones musicales lógicas.

- Canciones con mayor energía tienden a tener mayor volumen (energy ↔ loudness), lo que coincide con producciones orientadas a pista de baile.

- No existe una correlación significativa entre danceability y popularity, lo que indica que las canciones populares no necesariamente son las más bailables.

- La mayoría de canciones no son acústicas ni instrumentales.
acousticness e instrumentalness presentan valores muy bajos en mediana y cuartiles, mostrando predominancia de producciones electrónicas o con voz.

- En conjunto, el análisis revela que la popularidad de una canción no depende únicamente de sus características musicales cuantificables, sino probablemente de factores externos (marketing, artista, presencia en playlists, redes sociales, etc.).

- Este EDA es fundamental para una futura fase de modelado, donde se intentará predecir popularidad y analizar qué variables resultan más determinantes.

---

## Limitaciones del dataset y del análisis

- **Sesgo de selección y cobertura**: no está garantizado que el muestreo sea representativo de todo el catálogo de Spotify (puede estar sesgado por género, época o popularidad).
- **Popularidad dependiente del tiempo**: la métrica de `popularity` varía con el tiempo (lanzamientos, playlists, viralidad). El análisis es una “foto” estática y puede no reflejar tendencias actuales.
- **Faltan variables contextuales**: no incluye señales externas (campañas de marketing, presencia en playlists editoriales, seguidores del artista, país/mercado). Estas variables pueden explicar gran parte de la popularidad.
- **Calidad y consistencia de metadatos**: existen posibles errores o registros anómalos (por ejemplo, duraciones extremadamente altas). Requiere validación/adaptación previa al modelado.
- **Outliers y valores extremos**: se detectaron outliers especialmente en `duration_ms`. En este módulo (EDA) se documentan, pero su tratamiento se pospone para la etapa de modelado.
- **Multicolinealidad entre atributos de audio**: variables como `energy` y `loudness` están correlacionadas; esto puede afectar interpretaciones y algunos modelos si no se regulariza o seleccionan variables.
- **Escala y unidades heterogéneas**: los atributos mezclan escalas (0–1, BPM, dB, milisegundos). Para modelado será necesario estandarizar o normalizar.
- **Posibles duplicados/covers**: diferentes versiones o remasterizaciones pueden inflar conteos y sesgar métricas.
- **Generalización limitada**: los hallazgos describen este dataset concreto; no deben extrapolarse sin contrastar con otras fuentes o periodos.
- **No causalidad**: las correlaciones no implican causalidad; para conclusiones causales se requieren diseños o datos adicionales.

## Autor

**Anna Valencia**  
GitHub: https://github.com/annavalenciav





