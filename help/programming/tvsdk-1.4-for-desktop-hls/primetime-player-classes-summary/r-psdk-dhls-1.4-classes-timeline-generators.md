---
description: Estas clases ayudan a detectar oportunidades en una cronología para la ubicación del contenido, como los anuncios.
title: Clases de generadores de línea de tiempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Clases de generadores de línea de tiempo{#timeline-generators-classes}

Estas clases ayudan a detectar oportunidades en una cronología para la ubicación del contenido, como los anuncios.

Paquete: [com.adobe.mediacore.cronología.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Nombre | Descripción |
|---|---|
| [AdSignalingModeOportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | Clase que crea una oportunidad inicial para el modo de señalización de publicidad especificado. |
| [Generador de oportunidades](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Clase base para todos los generadores de oportunidades. |
| [Cliente de generador de oportunidades](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Interfaz utilizada por los generadores de oportunidades para comunicarse con los componentes de TVSDK. |
| [SpliceOutOportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | Clase que supervisa la cronología de reproducción y detecta las oportunidades de colocación de anuncios insertadas en el manifiesto como comentarios de SpliceOut. |
| [TimedMetadataOportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Implementación predeterminada de un generador de oportunidades que utiliza información de metadatos temporizada para detectar y generar oportunidades publicitarias. |