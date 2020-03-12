---
description: TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto, como los indicadores para un período de interrupción.
seo-description: TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto, como los indicadores para un período de interrupción.
seo-title: Generadores de oportunidades y solucionadores de contenido
title: Generadores de oportunidades y solucionadores de contenido
uuid: e1d658eb-cb6c-407d-9163-2dbf62ba1d19
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Generadores de oportunidades y solucionadores de contenido{#opportunity-generators-and-content-resolvers}

Un detector de oportunidades es un componente TVSDK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye un detector de oportunidades predeterminado:

* `PTOpportunityResolver`, que comprende las indicaciones de publicidad predeterminadas

TVSDK también incluye una resolución de contenido predeterminada que proporciona el contenido que se va a insertar en función de la clave de metadatos del elemento del reproductor:

* `PTContentResolver`

Puede anular los detectores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de la publicidad de las siguientes formas:

* Agregar compatibilidad con la detección de etiquetas personalizada
* Reconocer etiquetas personalizadas para la inserción de publicidades
* Crear un proveedor de publicidad personalizado
* Contenido de negro

TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto, como los indicadores para un período de interrupción.

Un *`opportunity`* representa un punto de interés en la cronología que generalmente indica una oportunidad de colocación de publicidad. Esta oportunidad también puede indicar una operación personalizada que podría afectar a la línea de tiempo, como un período de interrupción. An *`opportunity generator`* identifica las oportunidades específicas (etiquetas) en la línea de tiempo y notifica a TVSDK que estas oportunidades se han etiquetado. Las oportunidades se identifican en una línea de tiempo de `PTTimedMetadata` mediante la inclusión de una etiqueta no estándar (que no sea HLS).

Cuando se notifica a la aplicación sobre una oportunidad (etiqueta), la aplicación puede modificar la línea de tiempo; por ejemplo, insertando una serie de publicidades, cambiando a una secuencia alternativa (apagones) o editando de otro modo el contenido de la línea de tiempo. De forma predeterminada, TVSDK llama al equipo adecuado *`content resolver`* para implementar los cambios o acciones de línea de tiempo necesarios. La aplicación puede utilizar la resolución de contenido de publicidad TVSDK predeterminada o registrar su propia resolución de contenido.

También puede usar `PTSDKConfig.setAdTags` para agregar más etiquetas/indicaciones de marcadores de publicidad para que TVSDK pueda reconocer y usar `PTSDKConfig.setSubscribedTags` y notificar a la aplicación sobre etiquetas adicionales que podrían incluir información de flujo de trabajo de publicidad.

Un posible uso de una resolución personalizada es para períodos de interrupción. Para gestionar estos períodos, la aplicación podría implementar y registrar un detector de oportunidades de bloqueo que sea responsable de la gestión de etiquetas de bloqueo. Cuando TVSDK encuentra esta etiqueta, sondea todo el contenido registrado para encontrar el primero que maneja la etiqueta especificada. En este ejemplo, es la resolución de contenido de bloqueo la que puede, por ejemplo, reemplazar el elemento actual por contenido alternativo en el reproductor durante el tiempo especificado por la etiqueta .
