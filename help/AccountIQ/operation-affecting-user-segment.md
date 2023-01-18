---
title: Crear una operación en un segmento de usuario y realizar un seguimiento del efecto
description: Cómo crear una operación que afecte y rastree el efecto en un segmento definido de usuarios.
exl-id: ab74f857-e178-4120-8f9c-655ec921d096
source-git-commit: dd1001d94e32a1a8b5346ff97b0f6cb7d244dcf2
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# Creación de una operación en un segmento de usuario {#operation-to-track-segment}

Cada página de informes en Account IQ tiene un **Crear nueva operación** para ayudarle a crear flujos de trabajo que automatizan (y simplifican) diversas acciones (masivas) en cuentas de suscriptor; defina reglas para especificar una muestra, definir acciones y registrar y analizar los efectos de esas acciones. En la página para crear operaciones, puede definir la muestra de grupos de usuarios en los que se realizarán las operaciones y programar la operación para que se ejecute en una fecha futura.

Para crear una operación:

1. Defina su segmento (cohorte) para su análisis en cualquiera de las páginas de informes o tableros, siguiendo los pasos indicados en [Definición de segmentos y periodo de tiempo](/help/AccountIQ/howto-select-segment-timeframe.md).

1. Select **Crear nueva operación** disponible en cualquiera de las páginas de informes o tableros. La variable **Crear nueva operación** se muestra.

   ![Página para crear una nueva operación](assets/create-new-operations.png)
   *Figura: Página para crear una nueva operación*

1. En el **Crear nueva operación** rellene los detalles de los campos del formulario para:

   * [Nombre de la operación](#operation-details) en Detalles de operación
   * Segmento para ejecutar la operación en [Segmento de destino](#segment) y refinar el segmento utilizando [Segmentación adicional](#additional-segmentation)
   * [Tipo de segmento](#segment-type) under [Segmento de destino](#segment)
   * [Acción](#action)
   * [Activación de la programación](#schedule)

1. [Guardar la operación](#save-operation).

## Detalles de la operación {#operation-details}

+++Programador: detalles de operación

Asigne un nombre a la nueva operación en **Nombre de la operación** en Detalles de la operación. Por ejemplo, &quot;*Pruebe el efecto de la autenticación multifactor en los suscriptores de MVPD X&quot; o &quot;Limite el número de emisiones en la monitorización de concurrencia&quot; o &quot;Limita los suscriptores de MVPD que ven el canal &#39;N&#39; de más de 20 dispositivos*&quot;.

+++

+++MVPD: detalles de la operación

Asigne un nombre a la nueva operación en **Nombre de la operación** en Detalles de la operación. Por ejemplo, &quot;*Pruebe el efecto de la autenticación multifactor en los visores del canal N&quot; o &quot;Limite el número de emisiones en la supervisión de concurrencia&quot; o &quot;Limite los suscriptores que ven el canal &quot;N&quot; de más de 20 dispositivos*&quot;.

+++

## Segmento de destino {#segment}

+++Programador- Segmento de destino

La variable **Segmento** define a los usuarios a los que se aplicará esta operación; o el grupo de muestra para la operación. El segmento predeterminado es el **segmento** ha seleccionado mediante [panel de segmento y marco de tiempo](/help/AccountIQ/howto-select-segment-timeframe.md) en la página de informes o tableros principales del paso 1 anterior.

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

Este segmento define los suscriptores que se verán afectados por la operación que se está creando. Por ejemplo, el segmento seleccionado puede especificar *todas las cuentas de suscriptor de MVPD denominadas &#39;C&#39; que ven el canal &#39;N Sports&#39;*.

+++

+++MVPD: segmento de Target

La variable **Segmento** define a los usuarios a los que se aplicará esta operación; o el grupo de muestra para la operación. El segmento predeterminado es el **segmento** ha seleccionado mediante [panel de segmento y marco de tiempo](/help/AccountIQ/howto-select-segment-timeframe.md) en la página de informes o tableros principales del paso 1 anterior.

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

Este segmento define sus suscriptores (que son visualizadores de canales específicos) que se verán afectados por la operación que se está creando. Por ejemplo, su segmento (predeterminado) incluye *todas las cuentas de suscriptor que ven el canal &quot;N Sports&quot;*.
+++

### Segmentación adicional {#additional-segmentation}

Además, puede refinar el segmento de destino agregando más métricas. Por ejemplo, puede agregar otra métrica Probabilidad de uso compartido buena al 90 %. Así que ahora la declaración del problema dice: *&quot;cree una operación para cuentas de suscriptores de MVPD llamadas &#39;C&#39; que estén viendo el canal &#39;N Sports&#39; que tengan una probabilidad de compartir bueno 90%&quot;*.

![](assets/additional-segment.gif)

*Figura: Segmentación adicional*

Además, si refina la operación añadiendo otra métrica para el número de dispositivos, la declaración de problema actualizada dice *&quot;cree una operación para cuentas de suscriptores de MVPD llamadas &#39;C&#39; que estén viendo el canal &#39;N Sports&#39; que tengan una puntuación de uso compartido superior a 90 y que estén utilizando más de 5 dispositivos para ver contenido durante el periodo de evaluación&quot;*.

![](assets/refined-segment.png)

*Figura: Segmento de ejemplo refinado con puntuación de uso compartido general y número de métricas de dispositivos*

Al hacerlo, el grupo de usuarios se vuelve más refinado. Por lo tanto, al agregar más métricas y condiciones, califica aún más el segmento para definir las cuentas en las que se van a operar.

### Tipo de segmento {#segment-type}

Tipo de segmento es la forma en que se trata un segmento a lo largo del periodo de evaluación de la operación.

![](assets/segment-type.png)

*Figura: Refine el número de segmentos para operar usando el tipo de segmento*

<!--The segment type option allows you to further refine your segment based on the evaluation period (or time).

**Fixed number of accounts** 

When you select **Fixed number of accounts** segment type, then you need to specify an evaluation period as well.

By doing so, you are fixing the sample size for evaluation in terms of numbers. You are making Account IQ identify a specific set of users (that meet the criteria of defined evaluation period and segment metrics) to operate on. The analysis and graphs will be generated for this specific set of users only (identified initially) throughout the operation.

**Variable number of accounts**

When you select **Variable number of accounts** segment type, you do not limit the number of accounts in segment. The accounts which fall under the defined segment metrics are the part of the segment, and the number of accounts will change continuously during the course of operation.-->

>[!IMPORTANT]
>
>Solo puede usar **Número fijo de cuentas** a partir de ahora. La opción para seleccionar **Número variable de cuentas** estará disponible en próximas versiones.

<!--

you tell Account IQ in the beginning of the operation which number of accounts to operate on.

Account IQ system only has a segment definition, and during the operation it looks into all the accounts that fit that segments.

the number of accounts in segment is not limited, the accounts that fall under defined segment metrics will be part of the segment, and the no of accounts will change continuously, as there are no specific limitations - like an evaluation period in the past.When the segment is defined (which in this example is, subscriber accounts of MVPD 'C' who are viewing the channel 'N Sports' that have a sharing score above 80 and are using 10 different IPs) and we also identified a time period to evaluate a segment. This identifies X number of accounts as sample (for example 5000). How many devices they are using?
It identifies x-number of accounts (5000)...a very specific set of users that meet this criteria.
for every period that we schedule (within that operation) during that operation) we will look at those 5K users that are originally identified and we will present graph about them. How are the sharing scores coming up?u We identified a period. Are their sharing scores going up? Are there fewer of them who are meeting this definition?
Fixed versus variable is the way the treated in fixed or variable way.

1. we identified a fixed set of accounts.
2. we evaluate those specific accounts on criteria throughout the operation.

General idea independent of graph is that we will evaluate a set of accounts identified initially, for no of periods during operation and generate graphs against that.
Those are the 5000 users for which I will create graphs for for every period of the operation.

**Variable number of accounts**
We do not identify any initial set of accounts, we just have a segment definition.
Each period during the operation, we go and look into all the accounts that fit that segments.
If it is not a fixed segment, I won't initially evaluate it. I won't have an initial set of 5000. Instead at every period during the evaluation I will evaluate the segment then, and then I will produce graph about the next 3000 users.
the......will vary from period to period.

if not fixed segment, then I won't initially evaluate or have initial set of 5000, instead at every period during an operation and the.-->

## Acción {#action}

La variable **Acción** define qué operación realizará en el segmento definido.

Existen dos tipos de acciones que puede realizar:

* Acciones que utilizan sistemas integrados con Account IQ; como [Supervisión de la concurrencia](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)<!--, or Adobe Target-->.

* Acciones para crear y procesar flujos de trabajo externos a Account IQ y no integrados con el sistema de Account IQ. Por ejemplo, una acción para que el programador de canales &#39;N&#39; envíe correos electrónicos masivos a todos los suscriptores de MVPD &#39;C&#39;.

>[!NOTE]
>
>Al crear operaciones, no solo se especifican acciones y se define su ámbito, sino que también se empieza a registrar el efecto de estas operaciones.

## Programación{#schedule}

Puede programar la activación para la operación estableciendo las fechas de inicio y finalización.

>[!NOTE]
>
>La fecha de inicio y la fecha de finalización tienen una granularidad igual a la que seleccionó para la evaluación al definir el segmento mediante **panel de segmento y marco de tiempo**, en el paso 1.
>
>
>Por lo tanto, si seleccionó la granularidad como Semana, las fechas de inicio y finalización estarán en términos de semana (por ejemplo, Semana 14); si selecciona la granularidad como Mes, las fechas de inicio y finalización se expresan en términos de meses.


>[!IMPORTANT]
>
>La fecha de inicio debe ser posterior al periodo de evaluación y también posterior a la fecha actual. Del mismo modo, la fecha de finalización también debe ser posterior a la fecha de inicio y a la fecha actual.

### Guardar la operación {#save-operation}

Cuando guarda la operación, aparece una pantalla de mensaje que le informa de que el segmento que ha definido en esta operación también se guarda para el futuro. Sin embargo, debe asignar un nombre a este segmento.

![](assets/save-operation.png)

*Figura: Guardar operación y especificar el nombre del segmento*

>[!NOTE]
>
>Se recomienda nombrar la operación en función de la acción que esté realizando en combinación con el segmento en el que actuará.

<!--In future you can select this saved segment when defining a segment for your analysis on the main reports page. Moreover, the saved segment is also listed when you create an operation the next time.

![](assets/saved-segment-operations-page.png)

*Figure: Saved segments in segment selector on Create new operations page* 

>[!IMPORTANT]
>
>When creating an operation, if you select a segment that was previously created then you cannot add new metrics to it and refine it.
>
>Adding new metrics creates a new segment, but you cannot modify an existing segment.-->

Una vez creada una operación, se ejecutará desde la fecha de inicio hasta la fecha de finalización especificada.

Los detalles de la operación guardada se pueden ver en el [Operaciones](/help/AccountIQ/operations.md) página.

![](assets/new-operation-created.png)

*Figura: La operación recién creada se muestra en la página principal Operaciones*
