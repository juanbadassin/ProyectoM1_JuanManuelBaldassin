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
│   └── 3_WebScraping.ipynb  # Web scraping
├── Datasets/
│   ├── base_datos_restaurantes_USA_v2.csv   # Base original de clientes (30.000 × 17)
│   ├── clientes_miami.csv                   # Subconjunto filtrado (generado por 1_EDA)
│   ├── clientes_miami_limpio.csv            # Subconjunto limpio (generado por 1_EDA)
│   ├── yelp_restaurants.csv                 # Extracción de la API de Yelp (generado por 2_API_Yelp)
│   └── libros_scraping.csv                  # Resultado del web scraping
└── Documentacion/
    ├── README.pdf
    └── Recomendaciones.pdf
```

## Cómo ejecutar

1. Crear un entorno virtual e instalar dependencias:
   `pandas`, `numpy`, `matplotlib`, `requests`, `jupyter`.
2. Abrir los notebooks en orden (`1_` → `3_`). Todos son reproducibles sin
   credenciales porque los resultados intermedios están guardados en `Datasets/`.
3. **API de Yelp (opcional):** para re-extraer los datos, definir la variable de
   entorno `YELP_API_KEY` con una clave de [Yelp Fusion](https://www.yelp.com/developers)
   y poner `REEXTRAER = True` en `2_API_Yelp.ipynb`. La clave nunca se escribe en
   los notebooks ni se sube al repositorio.

## Hallazgos principales

- El cliente de **Miami** está por encima del promedio nacional en gasto,
  frecuencia de visita e ingresos; su preferencia dominante es **Mariscos**.
- El **estrato socioeconómico** es la variable que más explica el gasto:
  de $19/mes (Bajo) a $470/mes (Muy Alto), con correlación ingresos–gasto de 0,70.
- **Brecha de oferta**: 23% de los clientes de Miami es vegetariano y 12% vegano,
  pero solo 4,5% y 1% de los restaurantes atiende esas categorías.
- El top 10% de gasto no come distinto: **visita el doble y paga el triple** por comida.
