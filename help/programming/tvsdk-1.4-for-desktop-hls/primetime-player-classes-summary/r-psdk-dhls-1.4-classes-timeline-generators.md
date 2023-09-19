---
description: Estas clases ayudan a detectar oportunidades en una cronología para la colocación de contenido, como anuncios.
title: Clases de generadores de cronología
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Clases de generadores de cronología{#timeline-generators-classes}

Estas clases ayudan a detectar oportunidades en una cronología para la colocación de contenido, como anuncios.

Paquete: [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Nombre | Descripción |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | Clase que crea una oportunidad inicial para el modo de señalización de publicidad especificado. |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Clase base para todos los generadores de oportunidades. |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Interfaz utilizada por los generadores de oportunidades para comunicarse con componentes de TVSDK. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | Clase que supervisa la cronología de reproducción y detecta las oportunidades de colocación de anuncios insertadas en el manifiesto como comentarios SpliceOut. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Implementación predeterminada de un generador de oportunidades que utiliza información de metadatos cronometrados para detectar y generar oportunidades de publicidad. |
