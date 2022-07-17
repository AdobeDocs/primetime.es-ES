---
title: Ver informes en modo de aislamiento
description: 'Ver informes en modo de aislamiento para Xfinity. '
source-git-commit: afa77dd0d7ffe38d353fed21dc9591b994b11193
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Ver informes de uso compartido en modo de aislamiento {#report-isolation-mode}

En el modo de aislamiento, los MVPD (como Xfinity) identifican sistemáticamente a los suscriptores entre dispositivos, pero identifican a sus suscriptores de forma diferente en función de los programadores con los que interactúan. Mientras que en el modo estándar, los MVPD identifican constantemente a los suscriptores entre dispositivos, independientemente de los programadores.

Por ejemplo, en la siguiente imagen, si un suscriptor B de un MVPD de modo de aislamiento (como Xfinity) accede al contenido ofrecido por dos programadores diferentes utilizando el mismo dispositivo, entonces el MVPD asociará identificadores diferentes con los dos intentos de acceso diferentes. Por lo tanto, para esos programadores (L y M en la figura) y para Account IQ, parece que hay dos suscriptores diferentes que acceden al contenido. Sin embargo, para el MVPD estándar, si el suscriptor B accede al contenido ofrecido por dos programadores diferentes, entonces el MVPD asociará un único identificador de acceso para ambos intentos de acceso. Los MVPD (como Xfinity) en modo de aislamiento no identifican de forma consistente a un suscriptor aunque este esté utilizando el mismo dispositivo entre diferentes programadores.

![](assets/isolation-diff-new.png)

*Figura: El modo de aislamiento MVPD identifica cuatro suscriptores diferentes en lugar de dos*

Para administrar la distorsión de los datos (debido a la identificación del mismo suscriptor como diferente en función del acceso a diferentes programadores), el modo de aislamiento limita la actividad informada sobre un programador a la actividad solo en las aplicaciones de ese programador. Por ejemplo, para el modo de aislamiento en la imagen anterior, el programador L ve los datos basados únicamente en la actividad de las identidades W e Y, ignorando las identidades X y Z.

>[!IMPORTANT]
>
> El inconveniente es que el Programador L está privado de compartir información recopilada sobre los Suscriptores A y B debido a la actividad con cualquier Programador que no sea L.

En el modo de aislamiento, todos los cálculos realizados para obtener las puntuaciones de uso compartido y todas las métricas asociadas se realizan utilizando únicamente la actividad de los dispositivos que se transmiten desde aplicaciones pertenecientes al programador y los canales seleccionados.
Las puntuaciones y probabilidades de uso compartido solo se calculan utilizando el flujo que comienza desde los canales seleccionados actualmente.

Para ver las métricas en modo de aislamiento:

1. Select **modo de aislamiento** de la variable **MVPD en el segmento** y seleccione **Aplicar selección**.

   ![](assets/xfinity-in-segment.gif)

   *Figura: Selección de MVPD en modo de aislamiento*

1. Seleccione los canales que desee en el **Canales en el segmento** y seleccione **Aplicar selección**. Asimismo, seleccione un [lapso de tiempo](/help/AccountIQ/product-concepts.md#granularity-def).

   >[!IMPORTANT]
   >
   >Como el uso compartido de cuentas es más relevante cuando se mide para la transmisión por secuencias en todas las aplicaciones de los programadores, verá menores puntuaciones de uso compartido y algunas variaciones en las métricas en el modo de aislamiento.

   ![](assets/aggregate-sharing-isolation.png)

   *Figura: Uso compartido de indicadores de probabilidad en modo Aislamiento*

   Tenga en cuenta que los indicadores anteriores muestran que solo el 6 % de todas las cuentas se están compartiendo; y solo el 8% del contenido lo consumen ese 8%. De modo que los canales pueden comparar sus puntuaciones en el modo de aislamiento con las de los demás MVPD. Por lo tanto, la información obtenida utilizando el modo de aislamiento debe interpretarse de forma diferente a los demás datos.
