---
description: Un detector de oportunidades es un componente TVADK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y metadatos de la oportunidad de colocación.
seo-description: Un detector de oportunidades es un componente TVADK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y metadatos de la oportunidad de colocación.
seo-title: Personalización de detectores de oportunidades y resolución de contenido
title: Personalización de detectores de oportunidades y resolución de contenido
uuid: 7bd04c8f-6f04-4321-88e8-9bb93251d940
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Información general {#customize-opportunity-detectors-and-content-resolvers-overiew}

Un detector de oportunidades es un componente TVADK que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y metadatos de la oportunidad de colocación.

TVSDK incluye detectores de oportunidades predeterminados:

* `SpliceOutOpportunityDetector`, que comprende las indicaciones de publicidad predeterminadas
* `AdSignalingModeOpportunityGenerator`, que es responsable de crear las oportunidades iniciales de colocación de publicidad en función del modo de señalización de publicidad
* `SpliceOutOpportunityGenerator`, que es responsable de crear oportunidades de colocación de publicidad desde cualquier etiqueta #EXT-X-CUE

TVSDK también incluye una resolución de contenido predeterminada que proporciona el contenido que se va a insertar en función de la clave de metadatos del elemento del reproductor:

* `AuditudeResolver`, capaz de comunicarse con los servidores de decisiones de publicidad de Adobe Primetime (anteriormente conocidos como Auditude) y devolver saltos de publicidad para colocar.

Puede anular los detectores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de la publicidad de las siguientes formas:

* Añadir compatibilidad con la detección de etiquetas personalizada
* Reconocer etiquetas personalizadas para la inserción de publicidades
* Crear un proveedor de publicidad personalizado
* Contenido de negro

