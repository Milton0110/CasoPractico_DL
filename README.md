# Caso Práctico Deep Learning — Análisis de Reseñas Trustpilot

Análisis NLP de reseñas la empresa selecionada es "www.currys.co.uk", retailer perteneciente al sector de la electrónica. Comparado con 10 competidores del mismo sector.

El análisis responde a 4 preguntas planteadas por el director de Customer Experience:

1. ¿Las reseñas son positivas o negativas? ¿Y la competencia?
2. ¿Qué temas tratan? ¿Y la competencia?
3. Para cada tema, ¿cuál es el sentimiento predominante? ¿En qué somos mejores o peores?
4. ¿Cuáles son las principales áreas de mejora?

---

## Entregable

El fichero `analisis_currys.ipynb` se enecuentra dentro de la carpeta Solucion, y se debe respetar la estructura.

---

## Requisitos

**Python 3.10+** recomendado.Al realizar el proyecto se ha usado la version 3.12.9 

```bash
pip install -r requirements.txt
```

El modelo de sentimiento ([cardiffnlp/twitter-roberta-base-sentiment-latest](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest), ~500 MB) se descarga automáticamente de Hugging Face la primera vez que se ejecuta. Se necesita conexión a internet.

---

## Dataset

El dataset **no está incluido en el repositorio** (125 MB, supera el límite de GitHub).

Se puede descargar desde Kaggle:
**[Trustpilot Reviews 123k](https://www.kaggle.com/datasets/jerassy/trustpilot-reviews-123k)**

Una vez descargado, colócalo en la raíz del proyecto, **una carpeta por encima** del notebook:

```
CasoPractico_DL/
├── trustpilot-reviews-123k.csv   ← aquí
├── requirements.txt
├── README.md
└── Solucion/
    └── analisis_currys.ipynb
```

El notebook usa la ruta relativa `../trustpilot-reviews-123k.csv`, por lo que la estructura de carpetas debe respetarse.

---

## Cómo ejecutarlo

```bash
# 1. Clonar el repositorio
git clone https://github.com/Milton0110/CasoPractico_DL.git
cd CasoPractico_DL

# 2. Instalar dependencias
pip install -r requirements.txt

# 3. Descargar el dataset y colocarlo en la raíz del repositorio (ver sección Dataset)

# 4. Abrir el notebook
jupyter notebook Solucion/analisis_currys.ipynb
```

Ejecutar las celdas en orden. La sección 6 (inferencia RoBERTa sobre ~1.100 reseñas) tarda aproximadamente:

- **CPU**: 10–20 minutos
- **GPU**: 2–3 minutos

El resultado de la inferencia se guarda automáticamente en `Solucion/currys_with_sentiment.csv` para no tener que repetirla.

---

## Técnicas utilizadas

| Técnica                 | Detalle |
|---                      |---|
| Análisis de sentimiento | [RoBERTa — Cardiff NLP](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest) |
| Topic modeling          | NMF sobre TF-IDF (K=8, `random_state=42`) |
| Comparativa competencia | Gap de % positivo por topic (Currys − media 10 competidores) |

---

## Resultados principales

- Currys tiene **58% de reseñas negativas** — puesto 10 de 11 en el sector
- **Fortaleza relativa**: Atención al Cliente (+59.8 pp vs competencia)
- **Debilidad crítica**: Precio y Ofertas (−41.1 pp vs competencia)
- **Prioridades de mejora**: Garantía y Devoluciones (91% negativo) y Tienda Física (54% negativo, mayor volumen con 50 reseñas)
