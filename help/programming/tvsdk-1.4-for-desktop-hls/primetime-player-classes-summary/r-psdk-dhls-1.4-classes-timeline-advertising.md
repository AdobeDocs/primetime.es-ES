---
description: Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.
seo-description: Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.
seo-title: Clases de publicidad de línea de tiempo
title: Clases de publicidad de línea de tiempo
uuid: f424fa13-778b-458d-bc82-389441a8a56a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Clases de publicidad de línea de tiempo {#timeline-advertising-classes}

Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.

Paquete: [com.adobe.mediacore.tiempo.publicidad](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)Paquete: [com.adobe.mediacore.tiempo.publicidad.política](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nombre | Descripción |
|---|---|
| [Publicidad](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Clase que define la abstracción de publicidad y contiene toda la información de publicidad. Se define mediante un ID único, una duración y un `MediaResource`. El `MediaResource` contiene la dirección URL donde reside el contenido de la publicidad real. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Clase que representa un recurso que se va a mostrar. Clase que representa un recurso de publicidad. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Clase que proporciona una vista unificada de varias publicidades que se reproducirán en algún momento durante la reproducción. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumeración que define la directiva de reproducción de publicidad relacionada con el usuario que elude las publicidades al buscar. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Elemento de línea de tiempo asociado con la pausa publicitaria específica. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Clase de enumeración para directivas posibles sobre cuándo marcar una pausa publicitaria como observada. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Clase que representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Clase de enumeración para directivas posibles sobre dónde reanudar la reproducción de una pausa publicitaria después de la búsqueda o el modo de reproducción ficticia. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Clase de enumeración que enumera las formas en que se reproduce el reproductor, como la búsqueda o la reproducción normal. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaz que define propiedades para llamadas `AdPolicySelector` de API. Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Una interfaz de selector de directivas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden ajustarse a esta interfaz implementando todos los métodos requeridos o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Elemento de línea de tiempo asociado con una publicidad específica. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Clase que gestiona la resolución de anuncios en horario estelar en el proceso de TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumeración de todos los tipos de publicidad admitidos por el TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Clase. |

