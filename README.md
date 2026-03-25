# 📊 Customer Marketing Analysis — Power BI Dashboard

Análisis interactivo del comportamiento de compra de clientes a partir de un dataset de marketing, desarrollado como proyecto del módulo *Data Visualization with Power BI* del programa **Data-Driven Decision Specialist** en ESPOL Coding Bootcamps (Enero 2026).

---

## 🎯 Objetivo

Transformar datos de clientes en información accionable mediante dashboards interactivos, aplicando buenas prácticas de modelado de datos, DAX, visualización y storytelling analítico.

**Enfoque:** Perfil de cliente — identificar patrones de gasto, uso de descuentos y preferencias de canal según variables demográficas.

---

## 📁 Estructura del repositorio

```
├── CustomerMarketing_Dashboard.pbix   # Archivo Power BI
├── Informe_Final.pdf                  # Informe analítico completo
└── README.md
```

---

## ❓ Preguntas de negocio respondidas

| # | Pregunta | KPI |
|---|----------|-----|
| 1 | ¿Qué estado civil presenta mayor gasto promedio? | Ticket Promedio por Estado Civil |
| 2 | ¿Los clientes con hijos gastan más o menos? | Ticket Promedio por Composición del Hogar |
| 3 | ¿La gente que más gana prefiere un canal específico? | Ingreso Promedio por Canal Preferido |
| 4 | ¿Qué nivel educativo consume más productos premium? | Gasto Promedio en Premium por Nivel Educativo |
| 5 | ¿El uso de descuentos varía según la edad? | Promedio de Compras con Descuento por Rango Etario |

---

## 🧮 Medidas y columnas DAX destacadas

```dax
-- Ticket promedio por cliente
Ticket Promedio = AVERAGE('Dataset'[MntTotal])

-- Segmentación por presencia de hijos en el hogar
Categoría Hijos =
SWITCH(
    TRUE(),
    'Dataset'[Kidhome] = 0 && 'Dataset'[Teenhome] = 0, "Sin hijos",
    'Dataset'[Kidhome] > 0 && 'Dataset'[Teenhome] = 0, "Solo niños",
    'Dataset'[Kidhome] = 0 && 'Dataset'[Teenhome] > 0, "Solo adolescentes",
    'Dataset'[Kidhome] > 0 && 'Dataset'[Teenhome] > 0, "Niños y adolescentes"
)

-- Canal de compra preferido por cliente
CanalPreferido =
VAR Web = 'dataset'[NumWebPurchases]
VAR Store = 'dataset'[NumStorePurchases]
VAR Catalogo = 'dataset'[NumCatalogPurchases]
VAR MaxCompras = MAX(MAX(Web, Store), Catalogo)
RETURN
SWITCH(TRUE(),
    MaxCompras = Store, "Tienda Física",
    MaxCompras = Web, "Web",
    MaxCompras = Catalogo, "Catálogo",
    "Otros"
)

-- Segmentación por rango etario
Rango Edad =
SWITCH(
    TRUE(),
    'Dataset'[Age] < 35, "18–34 años",
    'Dataset'[Age] >= 35 && 'Dataset'[Age] < 50, "35–49 años",
    'Dataset'[Age] >= 50 && 'Dataset'[Age] < 65, "50–64 años",
    'Dataset'[Age] >= 65, "65+ años"
)
```

---

## 💡 Insights principales

- **Clientes viudos** presentan el mayor gasto promedio ($693,53), probablemente por tomar decisiones de compra de forma individual.
- **Clientes sin hijos** tienen el ticket más alto ($1.057,95); el gasto disminuye progresivamente a medida que el hogar incluye hijos.
- **El canal Catálogo** concentra a los clientes de mayor poder adquisitivo (ingreso promedio ~$71.700), lo que lo posiciona como el canal ideal para productos premium.
- **El nivel universitario** lidera el consumo de productos premium ($50,20 promedio), por encima de posgrado, maestría y doctorado.
- El **uso de descuentos aumenta con la edad**, con mayor frecuencia en el rango 50–64 años, lo que sugiere mayor sensibilidad al precio en ese segmento.

---

## 🛠️ Herramientas utilizadas

- Power BI Desktop
- DAX (medidas y columnas calculadas)
- Python (preprocesamiento del dataset)
- Excel (exploración de datos)

---
