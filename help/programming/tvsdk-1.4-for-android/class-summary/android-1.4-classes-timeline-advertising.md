---
description: Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.
title: Clases de publicidad de cronología
exl-id: fb31a235-6578-4da1-b732-713a2f9b24be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Clases de publicidad de cronología{#timeline-advertising-classes}

Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.

Paquete: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Paquete: [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nombre | Descripción |
|--- |--- |
| [Anuncio](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Clase que define la abstracción de publicidad y contiene toda la información de la publicidad. Se define mediante un ID único, una duración y un `MediaResource`. El `MediaResource` contiene la dirección URL donde reside el contenido del anuncio real. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Clase que representa un recurso que se va a mostrar. Clase que representa un recurso publicitario. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Clase que proporciona una vista unificada de varios anuncios que se reproducirán en algún momento durante la reproducción. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Clase de operación de colocación de pausa publicitaria. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Enumeración que define la política de reproducción de anuncios relacionada con el hecho de que el usuario omita los anuncios mientras busca. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Clase que representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interfaz que define propiedades para llamadas a la API AdPolicySelector. Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Una interfaz de selector de políticas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden ajustarse a esta interfaz implementando todos los métodos necesarios o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. |
| `auditude.AuditudeAdProvider` | Obsoleto. Utilice AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Clase que administra el horario de máxima audiencia y la resolución en el proceso de frases. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Clase que implementa la interfaz ContentTracker y define los eventos de seguimiento de anuncios de Primetime. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Clase que administra la parte de resolución de anuncios en el proceso de frases. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interfaz que define el protocolo que debe implementar si desea crear un módulo de seguimiento de anuncios diseñado para integrarse con la biblioteca o un rastreador de anuncios personalizado. Esta interfaz requiere que defina la forma en que se notifican los eventos de progreso de anuncio al sistema remoto de seguimiento de anuncios. |
| [PlacementInformation](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Clase que resume una solicitud de información de ubicación. Cada anuncio resuelto debe tener adjunta una información de ubicación. La información de ubicación describe dónde se pretende colocar el anuncio en la cronología. Contiene información como: <ul><li>Posición de colocación (en ms) </li><li>Tipo de ubicación (pre-roll, mid-roll o post-roll) </li><li>Duración del fragmento de contenido principal que se va a reemplazar</li></ul> |
