---
description: Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.
title: Clases publicitarias de la línea de tiempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# Clases publicitarias de línea de tiempo{#timeline-advertising-classes}

Estas clases proporcionan información sobre los anuncios que se producen dentro de una cronología.

Paquete: [com.adobe.mediacore.cronología.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Paquete: [com.adobe.mediacore.cronología.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nombre | Descripción |
|--- |--- |
| [Publicidad](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Clase que define la abstracción del anuncio y contiene toda la información del anuncio. Se define mediante un ID único, una duración y un `MediaResource`. El `MediaResource` contiene la dirección URL donde reside el contenido del anuncio real. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Clase que representa un recurso que se va a mostrar. Clase que representa un recurso de anuncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Clase que proporciona una vista unificada de varios anuncios que se reproducirán en algún momento durante la reproducción. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Clase de operación de colocación de pausa publicitaria. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Enumeración que define la política de reproducción de publicidad relacionada con el usuario que omite los anuncios al buscar. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Clase que representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interfaz que define propiedades para llamadas a la API AdPolicySelector . Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. |
| [Selector de políticas de publicidad](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Interfaz de selector de directivas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden ajustarse a esta interfaz implementando todos los métodos requeridos o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. |
| `auditude.AuditudeAdProvider` | Obsoleto. Utilice AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Clase que gestiona el primetime y la resolución en el proceso Frase. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Clase que implementa la interfaz ContentTracker y define los eventos de seguimiento de anuncios de Primetime. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Clase que gestiona la parte de resolución de anuncios en el proceso Frase. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interfaz que define el protocolo que debe implementar si desea crear un módulo de seguimiento de anuncios diseñado para integrarse con la biblioteca o un rastreador de anuncios personalizado. Esta interfaz requiere que defina la forma en que se informan los eventos de progreso de publicidad en el sistema de seguimiento de anuncios remoto. |
| [Información de ubicación](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Clase que abstrae una solicitud de información de ubicación. Cada anuncio resuelto debe tener una información de ubicación adjunta. La información de ubicación describe dónde se va a colocar el anuncio en la cronología. Contiene información como: <ul><li>Posición de colocación (en ms) </li><li>Tipo de colocación (anuncio previo a la emisión, anuncio intermedio o anuncio posterior) </li><li>Duración del fragmento de contenido principal que está a punto de reemplazarse</li></ul> |
