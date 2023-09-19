---
description: Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.
title: Clases de publicidad de cronología
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Clases de publicidad de cronología {#timeline-advertising-classes}

Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.

Paquete: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Paquete: [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nombre | Descripción |
|---|---|
| [Anuncio](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Clase que define la abstracción de publicidad y contiene toda la información de la publicidad. Se define mediante un ID único, una duración y un `MediaResource`. El `MediaResource` contiene la dirección URL donde reside el contenido del anuncio real. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Clase que representa un recurso que se va a mostrar. Clase que representa un recurso publicitario. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Clase que proporciona una vista unificada de varios anuncios que se reproducirán en algún momento durante la reproducción. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumeración que define la política de reproducción de anuncios relacionada con el hecho de que el usuario omita los anuncios mientras busca. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Elemento de cronología asociado con la pausa publicitaria específica. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Clase de enumeración para posibles directivas sobre cuándo marcar una pausa publicitaria como inspeccionada. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Clase que representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Clase de enumeración para posibles políticas sobre dónde reanudar la reproducción de una pausa publicitaria después del modo de búsqueda o truco-reproducción. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Clase de enumeración que enumera las formas en las que se reproduce el reproductor, como la llamada a otro punto del contenido o la reproducción normal. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaz que define propiedades para `AdPolicySelector` Llamadas de API. Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Una interfaz de selector de políticas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden ajustarse a esta interfaz implementando todos los métodos necesarios o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Elemento de cronología asociado a un anuncio específico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Clase que administra primetime y la resolución en el proceso de TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumeración de todos los tipos de anuncios admitidos por TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Clase. |
