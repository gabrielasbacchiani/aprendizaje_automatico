# Segmentación de clientes con K-Means

Actividad de la **Clase 8** de la materia **Aprendizaje Automático**, Tecnicatura en Ciencias de Datos e Inteligencia Artificial, Centro Politécnico Superior Malvinas Argentinas.

**Autora:** Gabriela Bacchiani

## Objetivo

Identificar segmentos latentes de clientes a partir de su comportamiento de compra y uso del sitio web, sin etiquetas previas, utilizando el algoritmo de aprendizaje no supervisado **K-Means**.

## Dataset

`dataset_segmentacion_clientes.csv`: 700 clientes y 7 variables numéricas, sin valores faltantes.

| Variable original | Nombre en el notebook | Descripción |
|---|---|---|
| `purchase_freq_month` | `frecuencia_compra_mes` | Compras por mes |
| `avg_basket_usd` | `ticket_promedio_usd` | Gasto promedio por compra (USD) |
| `time_on_site_min` | `tiempo_sitio_min` | Tiempo de permanencia en el sitio (minutos) |
| `discount_sensitivity` | `sensibilidad_descuentos` | Sensibilidad a descuentos (0 a 1) |
| `returns_rate` | `tasa_devoluciones` | Proporción de compras devueltas (0 a 0,8) |
| `noise_gauss` | `ruido_gauss` | Ruido aleatorio (excluida del modelo) |
| `noise_uniform` | `ruido_uniforme` | Ruido aleatorio (excluida del modelo) |

## Metodología

1. **Exploración de datos:** estadísticas descriptivas, histogramas y búsqueda de valores faltantes.
2. **Selección de variables:** se excluyeron las dos variables de ruido por no presentar estructura ni correlación con las demás.
3. **Escalado:** estandarización con `StandardScaler`, necesaria porque K-Means se basa en distancias y las variables tenían escalas muy distintas.
4. **Elección de k:** método del codo para k entre 2 y 6.
5. **Entrenamiento:** K-Means con k = 3, inicialización `k-means++` y `random_state=42` para reproducibilidad.
6. **Interpretación:** centroides en unidades originales y mapa de calor de centroides estandarizados.

## Resultados

Se identificaron **3 segmentos**:

| Segmento | Clientes | Frecuencia | Ticket | Tiempo en sitio | Estrategia sugerida |
|---|---|---|---|---|---|
| Frecuentes y comprometidos | 230 | ≈12 por mes | ≈180 USD | ≈35 min | Fidelización y recomendaciones personalizadas |
| Premium ocasionales | 250 | ≈2 por mes | ≈450 USD | ≈6 min | Upselling premium y aumento de frecuencia |
| Bajo ticket | 220 | ≈4 por mes | ≈90 USD | ≈10 min | Combos y promociones por monto mínimo |

Los segmentos se diferencian principalmente por la frecuencia de compra, el ticket promedio y el tiempo en sitio. La sensibilidad a descuentos y la tasa de devoluciones presentan valores similares en los tres grupos.

## Estructura del repositorio

```
├── Clase8_AA_Bacchiani.ipynb         # Notebook con el análisis completo
├── dataset_segmentacion_clientes.csv # Datos utilizados
└── README.md
```

## Cómo ejecutarlo

**En Google Colab:** abrir el notebook, subir el archivo CSV desde el panel de archivos (ícono de carpeta) y ejecutar todas las celdas.

**En local:** con Python 3 instalado,

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
jupyter notebook Clase8_AA_Bacchiani.ipynb
```

El CSV debe estar en la misma carpeta que el notebook.

## Tecnologías

Python · pandas · NumPy · Matplotlib · seaborn · scikit-learn
