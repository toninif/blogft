---
title: 'Tutorial: Nube de Palabras con `wordcloud2`'
author: "Fernando Tonini"
date: "2025-04-15"
excerpt: Así se puede hacer una nube de palabras.
slug: []
categories: []
tags:
- texto
- tutoriales
- nubes
- palabras
- wordclud
---

# Introducción

Una nube de palabras es una representación visual de la frecuencia de términos en un conjunto de texto. En este tutorial en castellano, aprenderás a crear tu propia nube de palabras a partir de canciones de cancha de Boca Juniors, utilizando el paquete `wordcloud2` en R.

# 1. Instalación

Antes de comenzar, asegúrate de tener instalado R y RStudio (opcional). Para instalar el paquete **wordcloud2**, ejecuta este comando en tu consola de R:

```r
# Instala desde CRAN (ejecutar en consola, no en este documento)
install.packages("wordcloud2")
```

# 2. Carga de paquetes

En tu documento `.qmd`, carga las librerías necesarias en un bloque de código:

```{r}
library(wordcloud2)
library(dplyr)
library(tidytext)
```

# 3. Datos de ejemplo: canciones de Boca Juniors

A continuación definimos un vector con fragmentos de canciones populares de la hinchada:

```{r}
canciones <- c(
  "Dale Boca, dale Boca, dale, dale campeón",
  "La Bombonera cada día late más",
  "Yo soy de Boca Juniors y te sigo a todas partes",
  "Oh, vamos Boca, muéstrales tu corazón",
  "Por estas calles siempre voy a volver",
  "El que no salta es un inglés",
  "Boca es mi pasión, mi locura y mi religión",
  "En las buenas y en las malas siempre presente",
  "Dale bostero, dale bostero, vos sos de Boca",
  "La 12 no se va, vive y siente la pasión",
  "Dale campeón, dale campeón, oooh campeón",
  "Cantemos todos juntos, vamos a ganar"
)
```

# 4. Preprocesamiento de texto

Convertimos los textos en tokens y calculamos la frecuencia de cada palabra:

```{r}
tokens <- tibble(texto = canciones) %>%
  unnest_tokens(palabra, texto) %>%
  count(palabra, sort = TRUE)

# Visualiza las primeras palabras más frecuentes
tokens %>% slice_max(n, n = 10)
```

# 5. Generación de la nube de palabras

Con los conteos listos, creamos la nube de palabras:

```{r}
wordcloud2(
  data = tokens,
  size = 0.7,
  color = "random-light",
  backgroundColor = "#003b7a"
)
```

> **Tip:** Se puede cambiar `size`, `color`, `backgroundColor` e incluso el `shape` (por ejemplo, `shape = "star"`) para personalizar tu nube.

# 6. Personalización avanzada

- **shape**: `wordcloud2(tokens, shape = "circle")`, `shape = "diamond"`, etc.
- **fontFamily**: `wordcloud2(tokens, fontFamily = "Courier New")`.
- **minRotation** y **maxRotation**: para variar la orientación de las palabras.

```{r}
# Ejemplo con forma de diamante y fuente específica
wordcloud2(tokens,
           size = 0.6,
           color = "random-dark",
           backgroundColor = "white",
           shape = "diamond",
           fontFamily = "Arial")
```

# Conclusión

Y ya esta! Así se hace una nube de palabras en R con `wordcloud2`.

---
**Referencias**

- Documentación oficial de **wordcloud2**: <https://cran.r-project.org/web/packages/wordcloud2/vignettes/wordcloud.html>
