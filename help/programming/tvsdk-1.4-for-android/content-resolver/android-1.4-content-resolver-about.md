---
description: Un detector de oportunidades es un componente de TVSDK que detecta las etiquetas personalizadas en un flujo e identifica las oportunidades de ubicación. Estas oportunidades se envían al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de ubicación.
title: Generadores de oportunidades y solucionadores de contenido
exl-id: e396eaa9-444d-4173-a534-74b29309a151
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Generadores de oportunidades y solucionadores de contenido {#opportunity-generators-and-content-resolvers}

Un detector de oportunidades es un componente de TVSDK que detecta las etiquetas personalizadas en un flujo e identifica las oportunidades de ubicación. Estas oportunidades se envían al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de ubicación.

TVSDK incluye un detector de oportunidades predeterminado:

* `SpliceOutPlacementOpportunityDetector`, que comprende las indicaciones de anuncios predeterminadas

TVSDK también incluye solucionadores de contenido predeterminados que proporcionan contenido para insertar en función de la clave de metadatos del elemento de reproductor:

* `AuditudeResolver` para `AUDITUDE_METADATA_KEY`, que es capaz de comunicarse con los servidores de Adobe Primetime ad Decisioning (anteriormente conocidos como Auditude) y devolver las pausas publicitarias que se van a publicar.

* `MetadataResolver` para `JSON_METADATA_KEY`

* `CustomAdMarkersContentResolver` para `TIME_RANGES_METADATA_KEY`

Puede anular los detectores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de publicidad de las siguientes maneras:

* Añadir compatibilidad con la detección de etiquetas personalizada
* Reconocimiento de etiquetas personalizadas para la inserción de anuncios
* Creación de un proveedor de publicidad personalizado
* Contenido en negro

TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la cronología, y estos generadores y solucionadores se basan en etiquetas no estándar en el manifiesto. Es posible que la aplicación tenga que modificar la cronología en función de las oportunidades identificadas en el manifiesto, como los indicadores de un periodo de interrupción.

Un *`opportunity`* representa un punto de interés en la cronología que generalmente indica una oportunidad de ubicación de publicidad. Esta oportunidad también puede indicar una operación personalizada que podría afectar a la cronología, como un periodo de interrupción. Un *`opportunity generator`* identifica oportunidades específicas (etiquetas) en la cronología y notifica a TVSDK que estas oportunidades se han etiquetado. Las oportunidades se identifican en una cronología en mediante la inclusión de una etiqueta no estándar (no HLS).

Cuando se notifica a la aplicación sobre una oportunidad (etiqueta), esta podría modificar la cronología, por ejemplo, insertando una serie de anuncios, cambiando a un flujo alternativo (interrupciones) o editando de otro modo el contenido de la cronología. De forma predeterminada, TVSDK llama al método apropiado *`content resolver`* para implementar los cambios o las acciones de cronología necesarios. Su aplicación puede utilizar la resolución de contenido de anuncios de TVSDK predeterminada o registrar su propia resolución de contenido.

También puede utilizar `MediaPlayerItemConfig.setAdTags` para añadir más etiquetas/indicaciones de marcador de anuncio para que TVSDK pueda reconocer y utilizar `MediaPlayerItemConfig.subscribedTags` y notifique a la aplicación sobre etiquetas adicionales que puedan tener información del flujo de trabajo de publicidad.

Un posible uso de una resolución personalizada es para periodos de interrupción. Para gestionar estos periodos, la aplicación podría implementar y registrar un detector de oportunidades de interrupción responsable de gestionar las etiquetas. Cuando TVSDK encuentra esta etiqueta, sondea todas las resoluciones de contenido registradas para encontrar la primera que administra la etiqueta especificada. En este ejemplo, es la resolución de contenido de la interrupción, que puede, por ejemplo, reemplazar el elemento actual con contenido alternativo en el reproductor durante la duración especificada por la etiqueta.
