---
description: Un detector de oportunidades es un componente TVSDK del explorador que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y metadatos de la oportunidad de colocación.
seo-description: Un detector de oportunidades es un componente TVSDK del explorador que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y metadatos de la oportunidad de colocación.
seo-title: Personalización de detectores de oportunidades y resolución de contenido
title: Personalización de detectores de oportunidades y resolución de contenido
uuid: d4926933-5966-4cd8-8050-c81c5e3c8545
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Información general {#customize-opportunity-detectors-and-content-resolvers-overview}

Un detector de oportunidades es un componente TVSDK del explorador que detecta etiquetas personalizadas en un flujo e identifica las oportunidades de colocación. Estas oportunidades se envían a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y metadatos de la oportunidad de colocación.

El SDK de explorador incluye los siguientes detectores de oportunidades predeterminados:

* `AdSignalingModeOpportunityGenerator`, que crea oportunidades de colocación de publicidad inicial basadas en el modo de señalización de publicidad.
* `ManifestCuesOpportunityGenerator`, que crea oportunidades de colocación de publicidad desde cualquier etiqueta de empalme.

El SDK de TVSDK de explorador también incluye los resueltores de contenido predeterminados, como `AuditudeResolver`, que proporcionan contenido que se insertará en función de la clave de metadatos del elemento del reproductor. `AuditudeResolver` puede comunicarse con los servidores de decisiones de publicidad de Adobe Primetime y devolver pausas publicitarias para colocarlas.

Puede anular los detectores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de la publicidad de las siguientes formas:

* Añadir compatibilidad con la detección de etiquetas personalizada
* Reconocer etiquetas personalizadas para la inserción de publicidades
* Crear un proveedor de publicidad personalizado

