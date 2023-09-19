---
description: Un detector de oportunidades es un componente TVSDK del explorador que detecta las etiquetas personalizadas en un flujo e identifica las oportunidades de ubicación. Estas oportunidades se envían al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de ubicación.
title: Personalizar detectores de oportunidades y solucionadores de contenido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Información general {#customize-opportunity-detectors-and-content-resolvers-overview}

Un detector de oportunidades es un componente TVSDK del explorador que detecta las etiquetas personalizadas en un flujo e identifica las oportunidades de ubicación. Estas oportunidades se envían al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de ubicación.

El TVSDK del explorador incluye los siguientes detectores de oportunidades predeterminados:

* `AdSignalingModeOpportunityGenerator`, que crea oportunidades de colocación de anuncios iniciales basadas en el modo de señalización de publicidad.
* `ManifestCuesOpportunityGenerator`, que crea oportunidades de colocación de anuncios a partir de cualquier etiqueta de empalme.

TVSDK del explorador también incluye solucionadores de contenido predeterminados, como `AuditudeResolver`, que proporciona contenido que se inserta en función de la clave de metadatos del elemento de reproductor. `AuditudeResolver` es capaz de comunicarse con los servidores de Adobe Primetime ad Decisioning y devolver las pausas publicitarias que deben colocarse.

Puede anular los detectores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de publicidad de las siguientes maneras:

* Añadir compatibilidad con la detección de etiquetas personalizada
* Reconocimiento de etiquetas personalizadas para la inserción de anuncios
* Creación de un proveedor de publicidad personalizado
