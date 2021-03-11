---
description: Un detector de oportunidades es un componente TVSDK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
title: Generadores de oportunidades y solucionadores de contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# Generadores de oportunidades y solucionadores de contenido {#opportunity-generators-and-content-resolvers}

Un detector de oportunidades es un componente TVSDK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye un detector de oportunidades predeterminado:

* `PTOpportunityResolver`, que comprende los avisos predeterminados

TVSDK también incluye una resolución de contenido predeterminada que proporciona contenido que se debe insertar en función de la clave de metadatos del elemento del reproductor:

* `PTContentResolver`

Puede anular los detectores de oportunidades predeterminados y los solucionadores de contenido para personalizar el flujo de trabajo de la publicidad de las siguientes maneras:

* Compatibilidad adicional con la detección de etiquetas personalizada
* Reconocer etiquetas personalizadas para la inserción de publicidad
* Crear un proveedor de publicidad personalizado
* Apagar contenido

<!--<a id="section_C2BA8F50230E4010ABFCD5D976BC1217"></a>-->

TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la cronología, y estos generadores y solucionadores se basan en etiquetas no estándar en el manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades que se identifican en el manifiesto, como los indicadores de un periodo de bloqueo.

Un *`opportunity`* representa un punto de interés en la cronología que normalmente indica una oportunidad de colocación de publicidad. Esta oportunidad también puede indicar una operación personalizada que podría afectar a la cronología, como un período de interrupción. Un *`opportunity generator`* identifica oportunidades específicas (etiquetas) en la cronología y notifica a TVSDK que estas oportunidades se han etiquetado. Las oportunidades se identifican en una cronología en `PTTimedMetadata` mediante la inclusión de una etiqueta no estándar (que no sea HLS).

Cuando se notifica a la aplicación sobre una oportunidad (etiqueta), la aplicación puede modificar la cronología; por ejemplo, insertando una serie de anuncios, cambiando a un flujo alternativo (interrupciones) o editando de otro modo el contenido de la cronología. De forma predeterminada, TVSDK llama al *`content resolver`* apropiado para implementar las acciones o cambios necesarios en la cronología. Su aplicación puede utilizar la resolución de contenido de publicidad TVSDK predeterminada o registrar su propia resolución de contenido.

También puede utilizar `PTSDKConfig.setAdTags` para agregar más etiquetas/indicaciones de marcadores de publicidad, de modo que el SDK de TVSDK pueda reconocer y utilizar `PTSDKConfig.setSubscribedTags` y notificar a la aplicación sobre etiquetas adicionales que podrían incluir información de flujo de trabajo de publicidad.

Un posible uso de una resolución personalizada es para periodos de interrupción. Para gestionar estos períodos, la aplicación podría implementar y registrar un detector de oportunidad de bloqueo responsable de gestionar las etiquetas de interrupción. Cuando TVSDK encuentra esta etiqueta, sondea a todos los solucionadores de contenido registrados para encontrar el primero que gestiona la etiqueta especificada. En este ejemplo, es la resolución de contenido de interrupción, que puede, por ejemplo, reemplazar el elemento actual con contenido alternativo en el reproductor durante el tiempo especificado por la etiqueta .