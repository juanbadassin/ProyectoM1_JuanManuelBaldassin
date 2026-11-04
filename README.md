# Proyecto Módulo 1 — Análisis de clientes de restaurantes (EE.UU.)

Proyecto integrador de Data Science: análisis de una base de 30.000 clientes de
restaurantes en 10 ciudades de EE.UU., enriquecido con datos reales de negocios
obtenidos de la API de Yelp.

**Autor:** Juan Manuel Baldassin

## Estructura

```
ProyectoM1_Baldassin/
├── Avances/Notebooks/
│   ├── 1_EDA.ipynb          # Carga, exploración, filtrado por Miami, limpieza y tabulación
│   ├── 2_API_Yelp.ipynb     # Conexión a la API de Yelp, extracción e integración con los clientes
│   ├── 3_graficos.ipynb     # Visualizaciones: ciudades, estratos, gasto, preferencias, membresías
│   ├── 3_WebScraping.ipynb  # Web scraping
│   ├── 4_Scraping_Wikipedia.ipynb  # Cultura de Miami desde Wikipedia + pasos extra con Selenium
│   └── capturas/            # Evidencia de la automatización con Selenium (4 capturas)
├── Datasets/
│   ├── base_datos_restaurantes_USA_v2.csv   # Base original de clientes (30.000 × 17)
│   ├── clientes_miami.csv                   # Subconjunto filtrado (generado por 1_EDA)
│   ├── clientes_miami_limpio.csv            # Subconjunto limpio (generado por 1_EDA)
│   ├── yelp_restaurants.csv                 # Extracción de la API de Yelp (generado por 2_API_Yelp)
│   ├── libros_scraping.csv                  # Resultado del web scraping
│   └── cultura_miami.csv                    # Sección Cultura del artículo de Miami en Wikipedia
└── Documentacion/
    ├── README.pdf
    └── Recomendaciones.pdf
```

## Cómo ejecutar

1. Crear un entorno virtual e instalar dependencias:
   `pandas`, `numpy`, `matplotlib`, `requests`, `beautifulsoup4`, `selenium`, `jupyter`
   (Selenium usa Microsoft Edge y descarga el driver automáticamente).
2. Abrir los notebooks en orden (`1_` → `4_`). Todos son reproducibles sin
   credenciales porque los resultados intermedios están guardados en `Datasets/`.
3. **API de Yelp (opcional):** para re-extraer los datos, poner `REEXTRAER = True`
   en `2_API_Yelp.ipynb`. La clave de entrenamiento provista por el curso está
   incluida en `yelp_api_key.txt` (raíz del repositorio) y el notebook la toma
   automáticamente; también puede definirse la variable de entorno `YELP_API_KEY`,
   que tiene prioridad.

## Avance 4 — Scraping de Wikipedia con IA + Selenium (descripción detallada)

**Generación con IA:** el script de `4_Scraping_Wikipedia.ipynb` fue generado con
**Claude (Anthropic)** a partir de las consignas, y luego revisado y ejecutado como
parte del proyecto.

**Parte 1 — Scraping de la cultura de Miami:** con `requests` + `BeautifulSoup` se
descarga el artículo de Miami en Wikipedia en español, se localiza la sección
*Cultura* y se extraen sus subsecciones (*Entretenimientos y artes escénicas*,
*Música popular*, *Medios de comunicación*) limpiando las marcas de referencia.
Resultado: **14 párrafos** guardados en `Datasets/cultura_miami.csv`.

**Parte 2 — Pasos extra con Selenium** (Microsoft Edge headless, driver automático),
cada paso verificado por código y documentado con captura en `Avances/Notebooks/capturas/`:
1. Acceso al artículo de **Miami** (`es.wikipedia.org/wiki/Miami`).
2. Búsqueda de **Chicago** (otra ciudad de la base) con el **buscador interno**.
3. Cambio del color del sitio a **"Oscuro"** — verificado por la clase
   `skin-theme-clientpref-night` del HTML (el default de Wikipedia es claro).
4. Cambio del **idioma** del artículo a **inglés** — verificado por la URL
   (`en.wikipedia.org`) y el atributo `lang="en"` del documento.

Notas técnicas documentadas: el buscador de Wikipedia reemplaza el campo de texto por
un componente dinámico al enfocarlo (hay que re-localizar el elemento), y la
preferencia de color se guarda por dominio (al saltar al artículo en inglés la página
vuelve al tema claro).

## Hallazgos principales

- El cliente de **Miami** está por encima del promedio nacional en gasto,
  frecuencia de visita e ingresos; su preferencia dominante es **Mariscos**.
- El **estrato socioeconómico** es la variable que más explica el gasto:
  de $19/mes (Bajo) a $470/mes (Muy Alto), con correlación ingresos–gasto de 0,70.
- **Brecha de oferta**: 23% de los clientes de Miami es vegetariano y 12% vegano,
  pero solo 4,5% y 1% de los restaurantes atiende esas categorías.
- El top 10% de gasto no come distinto: **visita el doble y paga el triple** por comida.
