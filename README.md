# Trabajo 2: Elección de la mejor tablet para el estudio y toma de apuntes en la universidad

-   **Autor:** Miguel Domínguez Jiménez
-   **Asignatura:** Teoría de Decisión
-   **Tema:** Elección de la mejor tablet para el estudio y toma de apuntes en la universidad.

------------------------------------------------------------------------

## Objetivo del Proyecto

Este repositorio contiene el trabajo práctico de la asignatura, cuyo objetivo es aplicar y comparar diversos métodos de decisión multicriterio para resolver el problema: **"Elección de la mejor tablet para el estudio y toma de apuntes en la universidad"**.

El análisis compara **4 alternativas (Tablets)**: \* A1: Apple iPad Air \* A2: Samsung Galaxy Tab S9 FE+ \* A3: Xiaomi Pad 6 \* A4: Microsoft Surface Go 4

La evaluación se basa en una jerarquía multinivel de 4 criterios principales y 8 subcriterios (Coste, Calidad de Lápiz, Calidad de Pantalla, Software, SO, Batería, Peso y Tamaño).

------------------------------------------------------------------------

## Contenido del Repositorio

Este proyecto RStudio contiene los siguientes ficheros:

-   `Trabajo 2.qmd`: Documento fuente Quarto. Contiene todo el código R, el análisis detallado y las conclusiones del trabajo.
-   `Trabajo 2.html`: Informe final renderizado (HTML), listos para su revisión.
-   `tablets.ahp`: Fichero de entrada (formato YAML) que define la jerarquía multinivel y las matrices de comparación 2 a 2 para el paquete `ahp`.
-   `teoriadecision_funciones_multicriterio.R`: Script con las funciones R base (AHP, ELECTRE, PROMETHEE).
-   `teoriadecision_funciones_multicriterio_utiles.R`: Script con funciones R de utilidad (tablas, gráficos).
-   `teoriadecision_funciones_multicriterio_diagram.R`: Script con funciones R para la creación de diagramas.

------------------------------------------------------------------------

## Metodología y Ejecución

El análisis completo se encuentra en el fichero `Trabajo 2.qmd` y sigue esta estructura metodológica:

1.  **AHP (Paquete `ahp`)**: Se carga el modelo desde `tablets.ahp` y se calculan los pesos globales y el ranking. Se realiza un análisis de consistencia de los juicios (ej. 1.9% en la matriz principal), validando los resultados.
2.  **AHP (Funciones R)**: Se replica el análisis manualmente definiendo todas las matrices de comparación 2 a 2 en R. Se vuelve a calcular la inconsistencia para cada matriz (`RI < 0.10`) y se confirma que el ranking final es idéntico al del paquete.
3.  **ELECTRE I**: Se aplica un análisis iterativo ("paso a paso"). La primera iteración elimina la `A4_Surface`. La segunda iteración, sobre el núcleo restante, concluye que `A1_iPad`, `A2_Samsung` y `A3_Xiaomi` son incomparables.
4.  **PROMETHEE II**: Se utiliza la función `multicriterio.metodo.promethee_windows` sobre los **datos originales** de las tablets (precio en €, Hz, etc.). Se definen funciones de preferencia (ej. "Linear" para Precio, "V-shape" para Lápiz) y se obtiene un ranking completo (`Xiaomi > iPad > Samsung > Surface`).
5.  **Conclusiones Comparativas**: Se justifica la diferencia en los resultados: AHP/PROMETHEE (métodos compensatorios) eligen `A3_Xiaomi` por su gran peso en `Precio`, mientras que ELECTRE (método no-compensatorio) declara un núcleo de 3 alternativas incomparables debido a vetos mutuos (Precio vs. Software/Lápiz).
