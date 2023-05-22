---
description: Un detector de oportunidades es un componente TVADK que detecta etiquetas personalizadas en un flujo e identifica oportunidades de ubicación. Estas oportunidades se envían al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de ubicación.
title: Personalizar detectores de oportunidades y solucionadores de contenido
exl-id: 0721278c-e128-4afc-ae81-4f23c2644859
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Información general {#customize-opportunity-detectors-and-content-resolvers-overiew}

Un detector de oportunidades es un componente TVADK que detecta etiquetas personalizadas en un flujo e identifica oportunidades de ubicación. Estas oportunidades se envían al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de ubicación.

TVSDK incluye detectores de oportunidades predeterminados:

* `SpliceOutOpportunityDetector`, que comprende las indicaciones de anuncios predeterminadas
* `AdSignalingModeOpportunityGenerator`, que es responsable de crear oportunidades de colocación de anuncios iniciales basadas en el modo de señalización de publicidad
* `SpliceOutOpportunityGenerator`, que es responsable de crear oportunidades de colocación de anuncios desde cualquier etiqueta de #EXT-X-CUE

TVSDK también incluye una resolución de contenido predeterminada que proporciona contenido para insertar en función de la clave de metadatos del elemento de reproductor:

* `AuditudeResolver`, capaz de comunicarse con los servidores de Adobe Primetime ad Decisioning (anteriormente conocidos como Auditude) y devolver las pausas publicitarias que se van a publicar.

Puede anular los detectores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de publicidad de las siguientes maneras:

* Añadir compatibilidad con la detección de etiquetas personalizada
* Reconocimiento de etiquetas personalizadas para la inserción de anuncios
* Creación de un proveedor de publicidad personalizado
* Contenido en negro
