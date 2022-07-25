---
title: Panel de Attribution IQ
description: El panel ayuda a identificar las instancias de uso compartido de contraseñas analizando una amplia gama de datos de suscriptores.
exl-id: 616da2a5-c9fe-40ea-90cf-f565bc13e764
source-git-commit: 32ba300ce729eab7a6906d8fb0875e8f2bbe2d1d
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# El tablero {#dashboard}

El panel resume y agrega datos en una colección de gráficos e informes diseñados para ofrecer una visión general de alto nivel del alcance y el impacto del uso compartido de cuentas. Proporciona una sola página que contiene los principales informes y métricas de Account IQ.

![tablero de cuentas IQ](assets/dashboard-capture.png)


*Figura: El tablero*

## Puntuación media de uso compartido: agregada para el segmento actual {#aggregated-sharing}

El panel Puntuación de uso compartido agregada proporciona una lectura de primera línea que resume la cantidad y el impacto del uso compartido en términos de cuentas y volumen de flujo continuo.

Los valores le ayudan a comprender la magnitud del uso compartido de credenciales por parte de sus suscriptores, lo que le proporciona una medida de la necesidad de actuar en consecuencia.

![](assets/aggregate-sharing-score.png)


*Figura: Panel Puntuación media de uso compartido: agregado para el segmento actual*

Las tres métricas siguientes son componentes de la puntuación media de uso compartido.

### Nivel de uso compartido {#sharing-level}

El indicador de nivel de uso compartido muestra el porcentaje de todas las cuentas de suscriptor (en el segmento definido) que se compartieron durante el lapso de tiempo seleccionado.

Un valor calculado basado en el promedio de la probabilidad de uso compartido calculada para cada cuenta del conjunto de MVPD seleccionados que se ha transmitido desde uno de los canales de programador seleccionados durante el lapso de tiempo seleccionado.

![](assets/sharing-level.png)


*Figura: Nivel de uso compartido*

El indicador de tendencias muestra el cambio porcentual en el valor de la métrica en respecto al lapso de tiempo anterior.

### Uso de cuentas compartidas {#usage-from-shared-accounts}

Este indicador indica qué porcentaje del uso de todas las cuentas de suscriptor proviene de las cuentas compartidas para el segmento y el periodo de tiempo definidos. El indicador marca los intervalos de uso (de cuentas compartidas) en la escala de 0 a 100%. Estos intervalos (denominados bajo, medio, alto y anormal) se basan en el promedio del sector.

También puede ver el indicador Tendencia , que muestra un aumento o una caída en el uso de cuentas compartidas en comparación con el lapso de tiempo anterior.

![](assets/usage-4mshared-accounts.png)


*Figura: Uso de cuentas compartidas*

### Puntuación de uso compartido general {#overall-sharing-score}

La puntuación general de uso compartido consiste en puntuaciones de uso compartido, que incluyen &quot;Nivel de uso compartido&quot; y &quot;z Uso de cuentas compartidas&quot;.

Proporciona un valor pensado para reflejar el impacto relativo del uso compartido en comparación con la industria. Su propósito es similar al de una puntuación de crédito, resumiendo la situación con un solo número. Pero en este caso, cuanto mayor sea el número, bueno será el daño potencial.

![](assets/overall-sharing-score.png)


*Figura: Puntuación de uso compartido general*

<!--### MVPDs in segment {#mvpd-in-segment}

It is a table of risk indices and accounts totals for the top MVPDs ranked by overall usage or account sharing.

![](assets/mvpds-in-segment.png)-->

### Puntuaciones generales de uso compartido en toda la industria para MVPD {#top-mvpds}

Esta tabla proporciona una vista comparativa de las diferentes puntuaciones de uso compartido agregadas para los MVPD en el segmento.

>[!NOTE]
>
>Esta tabla utiliza los datos generales del sector con fines comparativos, no los datos representados por esos MVPD en el segmento.

![](assets/top-mvpds.png)


*Figura: Principales MVPD en el segmento según la puntuación general*

### Puntuación de uso compartido por canales y MVPD {#sharin-score-by-channels-and-mvpds}

Esta tabla proporciona una vista comparativa del uso compartido de puntuaciones de los canales seleccionados para los MVPD en el segmento actual.

![](assets/sharing-scores-by-channels-mvpds.png)


*Figura: Uso compartido de puntuaciones por canales y MVPD*

### Probabilidad de uso compartido de cuentas {#accounts-sharing-probability}

Este gráfico divide las cuentas en intervalos de quintiles de probabilidad de uso compartido de muy baja (0-20%) a muy alta (80=100%).

>[!NOTE]
>
>El gráfico de barras utiliza una escala logarítmica.


![](assets/dashboard-ac-sharing-prob.png)


*Figura: Números y porcentajes de cuentas de suscriptor en diferentes intervalos de probabilidad de uso compartido*

### Número de cuentas y uso por nivel de probabilidad de uso compartido {#number-of-accounts-usage-sharing-probability}

Este panel proporciona una vista tabular de las cuentas divididas en rangos de quintiles de probabilidad de uso compartido de muy baja (0-20%) a muy alta (80-100%) con el uso asociado de cada quintil de cuentas compartidas.

![](assets/no-acc-usage-prob-level.png)


*Figura: Número de cuentas, tendencias y usos incluidos en varios intervalos de probabilidad*

