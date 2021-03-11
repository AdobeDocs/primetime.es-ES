---
description: Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.
title: Clases publicitarias de la línea de tiempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Clases publicitarias de línea de tiempo {#timeline-advertising-classes}

Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.

Paquete: [com.adobe.mediacore.cronología.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Paquete: [com.adobe.mediacore.cronología.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nombre | Descripción |
|---|---|
| [Publicidad](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Clase que define la abstracción del anuncio y contiene toda la información del anuncio. Se define mediante un ID único, una duración y un `MediaResource`. El `MediaResource` contiene la dirección URL donde reside el contenido del anuncio real. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Clase que representa un recurso que se va a mostrar. Clase que representa un recurso de anuncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Clase que proporciona una vista unificada de varios anuncios que se reproducirán en algún momento durante la reproducción. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumeración que define la política de reproducción de publicidad relacionada con el usuario que omite los anuncios al buscar. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Elemento de línea de tiempo asociado con la pausa publicitaria específica. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Clase de enumeración para políticas posibles sobre cuándo marcar una pausa publicitaria como observada. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Clase que representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Clase de enumeración para políticas posibles sobre dónde reanudar la reproducción de una pausa publicitaria después de la llamada a otro punto del contenido o del modo de reproducción. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Clase de enumeración que enumera las formas en que se reproduce el reproductor, como la búsqueda o la reproducción normal. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaz que define propiedades para llamadas de API `AdPolicySelector`. Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. |
| [Selector de políticas de publicidad](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaz de selector de directivas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden ajustarse a esta interfaz implementando todos los métodos requeridos o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Elemento de línea de tiempo asociado a un anuncio específico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Clase que gestiona la resolución de anuncios de primetime en el proceso TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumeración de todos los tipos de publicidad admitidos por el TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Clase. |

