---
description: Estas clases ayudan a detectar oportunidades en una cronología para la colocación de contenido, como los anuncios.
seo-description: Estas clases ayudan a detectar oportunidades en una cronología para la colocación de contenido, como los anuncios.
seo-title: Generadores de línea de tiempo, clases
title: Generadores de línea de tiempo, clases
uuid: 1e36b738-0684-44f0-b3c3-dd656c70f705
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# Generadores de línea de tiempo, clases{#timeline-generators-classes}

Estas clases ayudan a detectar oportunidades en una cronología para la colocación de contenido, como los anuncios.

Paquete: [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Nombre | Descripción |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | Clase que crea una oportunidad inicial para el modo de señalización de publicidad especificado. |
| [Generador de oportunidades](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Clase base para todos los generadores de oportunidades. |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Interfaz utilizada por los generadores de oportunidades para comunicarse con los componentes de TVSDK. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | Clase que supervisa la línea de tiempo de reproducción y detecta las oportunidades de colocación de anuncios insertadas en el manifiesto como comentarios de SpliceOut. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Implementación predeterminada de un generador de oportunidades que utiliza información de metadatos temporizados para detectar y generar oportunidades de publicidad. |