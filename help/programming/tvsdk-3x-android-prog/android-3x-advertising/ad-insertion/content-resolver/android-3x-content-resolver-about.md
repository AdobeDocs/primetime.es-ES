---
description: TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto, como los indicadores para un período de interrupción.
seo-description: TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto, como los indicadores para un período de interrupción.
seo-title: Generadores de oportunidades y solucionadores de contenido
title: Generadores de oportunidades y solucionadores de contenido
uuid: 5caf8924-3d76-45a1-a136-39932abe88b3
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Generadores de oportunidades y solucionadores de contenido {#opportunity-generators-and-content-resolvers}

TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto, como los indicadores para un período de interrupción.

Un *`opportunity`* representa un punto de interés en la cronología que generalmente indica una oportunidad de colocación de publicidad. Esta oportunidad también puede indicar una operación personalizada que podría afectar a la línea de tiempo, como un período de interrupción. Un *`opportunity generator`* identifica oportunidades específicas (etiquetas) en la línea de tiempo y notifica al TVSDK que estas oportunidades se han etiquetado. Las oportunidades se identifican en una línea de tiempo de, mediante la inclusión de una etiqueta no estándar (que no sea HLS).

Cuando se notifica a la aplicación sobre una oportunidad, la aplicación puede modificar la línea de tiempo insertando una serie de publicidades, cambiando a un flujo alternativo (apagones) o editando de otro modo el contenido de la línea de tiempo. De forma predeterminada, TVSDK llama al *`content resolver`* apropiado para implementar las acciones o cambios de línea de tiempo necesarios. La aplicación puede utilizar la resolución de contenido de publicidad TVSDK predeterminada o registrar su propia resolución de contenido.

También puede utilizar `MediaPlayerItemConfig.setAdTags` para agregar más indicaciones/etiquetas de marcadores de publicidad, de modo que TVSDK pueda reconocer y utilizar `MediaPlayerItemConfig.subscribedTags` y notificar a la aplicación sobre etiquetas adicionales que podrían tener información de flujo de trabajo de publicidad.

Un posible uso de una resolución personalizada es para períodos de interrupción. Para gestionar estos períodos, la aplicación podría implementar y registrar un detector de oportunidades de bloqueo que sea responsable de la gestión de etiquetas de bloqueo. Cuando TVSDK encuentra esta etiqueta, sondea todo el contenido registrado para encontrar el primero que maneja la etiqueta especificada. En este ejemplo, es la resolución de contenido de bloqueo la que puede, por ejemplo, reemplazar el elemento actual por contenido alternativo en el reproductor durante el tiempo especificado por la etiqueta .