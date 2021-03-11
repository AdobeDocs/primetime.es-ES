---
description: Un detector de oportunidades es un componente TVSDK del explorador que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
title: Personalización de detectores de oportunidades y resolución de contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Información general {#customize-opportunity-detectors-and-content-resolvers-overview}

Un detector de oportunidades es un componente TVSDK del explorador que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían al gestor de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

El SDK de explorador incluye los siguientes detectores de oportunidad predeterminados:

* `AdSignalingModeOpportunityGenerator`, que crea oportunidades de colocación de anuncios iniciales basadas en el modo de señalización de anuncios.
* `ManifestCuesOpportunityGenerator`, que crea oportunidades de colocación de anuncios desde cualquier etiqueta de salida de empalme.

El SDK de TVSDK del explorador también incluye los solucionadores de contenido predeterminados, como `AuditudeResolver`, que proporcionan contenido que se insertará en función de la clave de metadatos del elemento del reproductor. `AuditudeResolver` es capaz de comunicarse con los servidores de Adobe Primetime ad decisioning y devolver pausas publicitarias que se van a colocar.

Puede anular los detectores de oportunidades predeterminados y los solucionadores de contenido para personalizar el flujo de trabajo de la publicidad de las siguientes maneras:

* Compatibilidad adicional con la detección de etiquetas personalizada
* Reconocer etiquetas personalizadas para la inserción de publicidad
* Crear un proveedor de publicidad personalizado

