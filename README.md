# Análisis de Embudo de Ventas y Test A/A/B (Aplicación Móvil de E-commerce)

## Descripción del Proyecto
Este proyecto, desarrollado durante mi formación en Data Analytics, investiga el comportamiento del usuario en una aplicación móvil de venta de productos alimenticios. Se centra en el análisis detallado del embudo de ventas y la evaluación de los resultados de un test A/A/B diseñado para optimizar el diseño de la interfaz de usuario (fuentes).

## Problema de Negocio / Objetivo
Una empresa emergente busca optimizar su aplicación móvil. Para ello, se planteó:
1.  **Estudiar el embudo de ventas:** Comprender las etapas clave que los usuarios atraviesan hasta la compra, identificar puntos de fricción y calcular tasas de conversión entre etapas.
2.  **Evaluar un cambio de diseño de interfaz (fuentes):** Determinar si un nuevo conjunto de fuentes en la aplicación afecta negativamente el comportamiento del usuario mediante un test A/A/B riguroso.
3.  **Validar la robustez de los mecanismos de prueba:** Utilizar los grupos A/A para asegurar que los resultados de futuros experimentos sean fiables.
4.  **Tomar una decisión basada en datos:** Recomendar si implementar o no el nuevo diseño de fuentes.

## Conjunto de Datos
El análisis se basó en un único dataset de logs de eventos de usuario:
* **`logs_exp_us.csv`**: Cada registro es una acción de usuario o un evento.
    * `EventName`: Nombre de la acción (ej. `MainScreenAppear`, `CartScreenAppear`, `PaymentScreenSuccessful`).
    * `DeviceIDHash`: Identificador único de usuario.
    * `EventTimestamp`: Hora del evento.
    * `ExpId`: Número de experimento (246 y 247 son grupos de control, 248 es grupo de prueba).

## Herramientas y Tecnologías Utilizadas
* **Python:** Lenguaje principal para la manipulación, limpieza, análisis estadístico y visualización de datos.
    * `pandas`: Esencial para la gestión de datos, manipulación de fechas y agregaciones.
    * `numpy`: Para operaciones numéricas.
    * `matplotlib` / `seaborn`: Para la creación de histogramas, embudos de conversión y gráficos comparativos.
    * `scipy.stats`: Fundamental para realizar pruebas de significancia estadística (ej. prueba de Z para proporciones).
* **Jupyter Notebook - VSCode:** Entorno de desarrollo interactivo para el análisis y la presentación organizada de los resultados.

## Metodología y Análisis
### Parte 1: Estudio del Embudo de Eventos
1.  **Preparación de Datos:** Carga del dataset, limpieza de nombres de columnas, verificación de tipos de datos, tratamiento de valores ausentes y adición de columnas de fecha/hora.
2.  **Comprobación de Datos:** Análisis de la cantidad de eventos y usuarios, promedio de eventos por usuario, y rango de tiempo cubierto por los datos. Identificación y exclusión de datos incompletos o sesgados al inicio del período.
3.  **Construcción del Embudo:** Identificación de eventos únicos y su frecuencia. Ordenación de eventos por número de usuarios y cálculo de la proporción de usuarios que realizan cada acción.
4.  **Análisis de Flujo:** Determinación de la secuencia de eventos más probable para el embudo de ventas (ej. `MainScreenAppear` → `OffersScreenAppear` → `CartScreenAppear` → `PaymentScreenSuccessful`).
5.  **Puntos de Fuga:** Identificación de las etapas donde se pierde el mayor porcentaje de usuarios y cálculo del porcentaje de usuarios que completan el viaje hasta el pago.

### Parte 2: Análisis del Test A/A/B
1.  **Composición de Grupos:** Verificación del número de usuarios en cada grupo experimental (246, 247, 248) y confirmación de que no hay usuarios en múltiples grupos.
2.  **Validación del Test A/A:**
    * Comparación estadística de los grupos de control (246 y 247) para el evento más popular y otros eventos clave, utilizando pruebas de significancia estadística (ej., prueba Z para proporciones).
    * Objetivo: Confirmar que no hay diferencias estadísticamente significativas entre los grupos de control, lo que valida la correcta división de la muestra y la fiabilidad del mecanismo de prueba.
3.  **Comparación A/B:**
    * Comparación estadística del grupo de prueba (248) con cada uno de los grupos de control (246 y 247) de forma aislada para cada evento.
    * Comparación del grupo de prueba (248) con los grupos de control combinados (246 + 247) para obtener una visión general.
    * **Nivel de Significancia (Alpha):** Discusión sobre el ajuste del nivel de significancia para múltiples pruebas de hipótesis (ej., corrección de Bonferroni si se consideró).


<img width="1058" height="153" alt="image" src="https://github.com/user-attachments/assets/be0b66ad-2547-48d2-9e96-9b69fe5802d9" />

<img width="1330" height="556" alt="image" src="https://github.com/user-attachments/assets/2a96cf7f-9046-406f-a173-68a80ecae8ba" />

<img width="646" height="555" alt="image" src="https://github.com/user-attachments/assets/6e188a6c-fd06-4f46-96e7-fe6f789cba28" />

<img width="798" height="555" alt="image" src="https://github.com/user-attachments/assets/a9698b32-6f44-4b58-8b87-cfe2fed3cc61" />






* comparado con los grupos de control / **sí tuvo un impacto significativo y positivo/negativo** en X métrica].
* **Decisión:** Basado en estos resultados, se recomendó [No implementar el nuevo diseño de fuentes, ya que no produce mejores resultados o genera una caída / Implementar el nuevo diseño de fuentes si los resultados son positivos / Continuar el test si no hay una conclusión clara].
