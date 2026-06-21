# Caso Práctico Deep Learning — Análisis de Reseñas Trustpilot

Análisis NLP de reseñas de **www.currys.co.uk** (mayor retailer de electrónica del UK) comparado con 10 competidores del mismo sector.

Responde a 4 preguntas planteadas por el director de Customer Experience:
1. ¿Las reseñas son positivas o negativas? ¿Y la competencia?
2. ¿Qué temas tratan? ¿Y la competencia?
3. Para cada tema, ¿cuál es el sentimiento predominante? ¿En qué somos mejores o peores?
4. ¿Cuáles son las principales áreas de mejora?

---

## Entregables

| Fichero | Descripción |
|---|---|
| `analisis_currys.ipynb` | Notebook de entrega — análisis limpio y ejecutable |
| `analisis_currys_estudio.ipynb` | Notebook de estudio — mismo análisis con explicaciones teóricas |
| `Presentacion_Currys.pptx` | Presentación con resultados (11 diapositivas) |

---

## Requisitos

**Python 3.10+** recomendado.

```bash
pip install -r requirements.txt
```

El modelo de sentimiento (`cardiffnlp/twitter-roberta-base-sentiment-latest`, ~500 MB) se descarga automáticamente de Hugging Face la primera vez que se ejecuta la celda correspondiente. Se necesita conexión a internet.

---

## Dataset

El dataset **no está incluido en el repositorio** (125 MB, supera el límite de GitHub).

Descárgalo desde Kaggle:  
**[Trustpilot Reviews 123k — kaggle.com/datasets/...](https://www.kaggle.com)**  
*(buscar: "trustpilot reviews 123k")*

Una vez descargado, colócalo **una carpeta por encima** de los notebooks:

```
Proyecto/
├── trustpilot-reviews-123k.csv   ← aquí
├── requirements.txt
├── README.md
└── Solucion/
    ├── analisis_currys.ipynb
    ├── analisis_currys_estudio.ipynb
    └── Presentacion_Currys.pptx
```

Los notebooks usan la ruta relativa `../trustpilot-reviews-123k.csv`, por lo que la estructura de carpetas debe respetarse exactamente.

---

## Reproducir el análisis

```bash
# 1. Clonar el repositorio
git clone https://github.com/Milton0110/CasoPractico_DL.git
cd CasoPractico_DL

# 2. Instalar dependencias
pip install -r requirements.txt

# 3. Colocar el dataset en la carpeta padre (ver sección Dataset)

# 4. Abrir el notebook
jupyter notebook analisis_currys.ipynb
```

Ejecutar las celdas en orden. La sección 6 (inferencia RoBERTa sobre ~1.100 reseñas) tarda:
- **CPU**: ~10–20 minutos
- **GPU**: ~2–3 minutos

El resultado de la inferencia se guarda en `Solucion/currys_with_sentiment.csv` para no tener que repetirla.

---

## Técnicas utilizadas

| Técnica | Detalle |
|---|---|
| Análisis de sentimiento | RoBERTa (`cardiffnlp/twitter-roberta-base-sentiment-latest`) |
| Topic modeling | NMF sobre TF-IDF (K=8, `random_state=42`) |
| Comparativa competencia | Gap de % positivo por topic (Currys − media 10 competidores) |

---

## Resultados principales

- Currys tiene **58% de reseñas negativas** — puesto 10 de 11 empresas del sector
- **Fortaleza**: Atención al Cliente (+59.8 pp vs competencia)
- **Debilidad crítica**: Precio y Ofertas (−41.1 pp vs competencia)
- **Prioridad de mejora**: Garantía y Devoluciones (91% negativo) y Tienda Física (54% negativo, 50 reseñas)
