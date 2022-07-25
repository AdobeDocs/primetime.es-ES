---
title: Definir un segmento y un lapso de tiempo
description: Definir un segmento y un lapso de tiempo
exl-id: 86fe010d-3202-4ce2-b803-ff44f5538d7e
source-git-commit: 037c65b28d3c4d7f09bde89e3a9d4bae86f6f867
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Definir un segmento y un lapso de tiempo {#define-segment}

Todos los análisis o la visualización de informes en Account IQ comienzan con la definición del segmento y la selección del lapso de tiempo para la evaluación. [Segmento](/help/AccountIQ/product-concepts.md#segmet-def) hace referencia a todos los suscriptores o visualizadores que cumplen con sus criterios (suscripción a un MVPD y visualización de canales específicos) de evaluación.

![](assets/segment-panel.png)

*Figura: Selección de segmentos y lapsos de tiempo*

En la parte superior de todas las páginas de informes de Account IQ, hay un panel para definir el segmento seleccionando MVPD, programadores de canales, granularidad y lapso de tiempo.

## Selección de segmentos {#select-segment}

### Seleccionar MVPD en el segmento {#select-segment-mvpds}

Para seleccionar MVPD de **MVPD en el segmento** opción:

1. Toque o haga clic en **MVPD en el segmento** opción desplegable.

   >[!NOTE]
   >
   >**Todo** los MVPD del sector están seleccionados de forma predeterminada. Desde aquí puede seleccionar cualquiera de los **Principales 10 MVPD compartiendo la puntuación**, **Principales 10 MVPD por uso**, **Principales 10 MVPD por cuentas** o MVPD individuales. Sin embargo, para seleccionar MVPD individuales debe anular la selección **Todo**.

1. Toque o haga clic en los MVPD deseados.

   Puede quitar un MVPD de la selección anulando la selección.

1. Toque o haga clic en **Aplicar selección** para que su selección tenga efecto. De lo contrario, perderá la selección que haya realizado.

   >[!NOTE]
   >
   >Si selecciona el modo de aislamiento, no se puede seleccionar ninguno de los demás MVPD.

### Seleccionar canales en un segmento {#select-segment-channels}

Para seleccionar los canales de programador que desee en el **Canales en el segmento** opción:

1. Toque o haga clic en **Canales en el segmento** opción desplegable.

   >[!NOTE]
   >
   >**Todo** los canales del programador de su empresa están seleccionados de forma predeterminada. Para seleccionar canales o programadores individuales, primero debe anular la selección **Todo**.

1. Toque o haga clic en los canales o programadores deseados.

   Los elementos de lista de nivel superior de la variable **Canales en el segmento** are [programador](/help/AccountIQ/product-concepts.md#programmer-def) las compañías y los elementos de la lista bajo nombres de programadores son sus [canales](/help/AccountIQ/product-concepts.md#channel-def). Puede seleccionar canales individuales en programadores, o seleccionar programadores y todas las actividades de los canales bajo ese programador se incluyen en los resultados de informes y gráficos.

   ![](assets/programmer-channels.png)


   *Figura: Programadores y canales enumerados en el selector de canales*

   >[!IMPORTANT]
   >
   >Los resultados de seleccionar canales individuales bajo un programador no son los mismos que los de seleccionar al programador.
   >
   >
   >Al seleccionar canales individuales, las actividades de esos canales se desglosan individualmente en algunos informes. Sin embargo, cuando selecciona el programador principal de todos esos canales, se incluye toda la actividad de esos canales, pero no se desglosa de forma individual en los informes.

1. Toque o haga clic en **Aplicar selección** para que su selección tenga efecto.

>[!NOTE]
>
>No puede seleccionar más de 10 elementos en los menús desplegables de MVPD o programador.

### Anule la selección de MVPD y canales {#deselect-segment-mvpds-channels}

Además de cambiar la selección en el **MVPD en el segmento** y **Canales en el segmento** selectores de segmentos, puede anular la selección de los MVPD y canales seleccionados anteriormente mediante:

* Al seleccionar la variable **Eliminar** icono (![icono quitar](assets/remove-icon.png)) en los nombres de estos MVPD y canales seleccionados que se muestran debajo del selector de segmentos.

* También puede utilizar **Borrar selección** para eliminar todos los MVPD o canales seleccionados previamente.

![](assets/segment-panel-selection1.png)

*Figura: MVPD y canales seleccionados en el panel de segmentos y marcos de tiempo*

![](assets/segment-panel-selection.png)

*Figura: MVPD y canales seleccionados en el panel de segmentos y marcos de tiempo*

## Granularidad y selección de lapso de tiempo {#granularity-timeframe}

Para seleccionar un período de tiempo de evaluación:

1. Seleccione el **Granularidad y lapso de tiempo** selector de fechas.

1. Seleccione: **Semana** o **Mes** from **Agregar por** para establecer la granularidad en la evaluación.

   ![](assets/granularity-timeframe-weekwise.png)


   *Figura: Selector de fecha para seleccionar Granularidad y lapso de tiempo*

1. Una vez seleccionada la granularidad, puede utilizar flechas hacia adelante o hacia atrás para avanzar o retroceder en el tiempo.

1. Especifique un periodo de tiempo en el pasado (en mes o semana según la granularidad seleccionada) para la evaluación.

1. Select **Aplicar selección** para asegurarse de que la selección surta efecto.
