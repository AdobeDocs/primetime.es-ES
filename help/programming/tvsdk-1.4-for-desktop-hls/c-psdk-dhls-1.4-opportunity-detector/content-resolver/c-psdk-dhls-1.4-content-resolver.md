---
description: Un detector de oportunidades es un componente TVADK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
title: Personalización de detectores de oportunidades y resolución de contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Información general {#customize-opportunity-detectors-and-content-resolvers-overiew}

Un detector de oportunidades es un componente TVADK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye detectores de oportunidad predeterminados:

* `SpliceOutOpportunityDetector`, que comprende los avisos predeterminados
* `AdSignalingModeOpportunityGenerator`, que es responsable de crear oportunidades de colocación de publicidad inicial basadas en el modo de señalización de publicidad
* `SpliceOutOpportunityGenerator`, que es responsable de crear oportunidades de colocación de anuncios a partir de cualquier etiqueta #EXT-X-CUE

TVSDK también incluye una resolución de contenido predeterminada que proporciona contenido que se debe insertar en función de la clave de metadatos del elemento del reproductor:

* `AuditudeResolver`, capaz de comunicarse con los servidores de Adobe Primetime ad decisioning (anteriormente conocidos como Auditude) y devolver pausas publicitarias que se van a colocar.

Puede anular los detectores de oportunidades predeterminados y los solucionadores de contenido para personalizar el flujo de trabajo de la publicidad de las siguientes maneras:

* Compatibilidad adicional con la detección de etiquetas personalizada
* Reconocer etiquetas personalizadas para la inserción de publicidad
* Crear un proveedor de publicidad personalizado
* Apagar contenido

