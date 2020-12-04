---
description: Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.
seo-description: Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.
seo-title: Clases de publicidad de línea de tiempo
title: Clases de publicidad de línea de tiempo
uuid: 4e6ca9fb-9e68-4625-a24b-386a50333862
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Clases publicitarias de escala de tiempo{#timeline-advertising-classes}

Estas clases proporcionan información sobre las publicidades que se producen dentro de una línea de tiempo.

Paquete: [com.adobe.mediacore.timeline.publicidad](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Paquete: [com.adobe.mediacore.timeline.publicidad.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nombre | Descripción |
|--- |--- |
| [Publicidad](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Clase que define la abstracción de publicidad y contiene toda la información de publicidad. Se define mediante un identificador único, una duración y un `MediaResource`. El `MediaResource` contiene la dirección URL donde reside el contenido de la publicidad real. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Clase que representa un recurso que se va a mostrar. Clase que representa un recurso de publicidad. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Clase que proporciona una vista unificada en varios anuncios que se reproducirán en algún momento durante la reproducción. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Clase de operación de colocación de pausa publicitaria. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Lista desglosada que define la directiva de reproducción de publicidad relacionada con el usuario que omite las publicidades mientras realiza la búsqueda. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Clase que representa una instancia de clic asociada a un recurso. Esta instancia contiene información sobre la URL de pulsación y el título que se puede utilizar para proporcionar información adicional al usuario. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interfaz que define las propiedades de las llamadas de API de AdPolicySelector. Estas propiedades proporcionan el contexto para aplicar cada comportamiento publicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Una interfaz de selector de directivas de publicidad para aplicar comportamientos de publicidad. Las aplicaciones pueden ajustarse a esta interfaz implementando todos los métodos requeridos o ampliando la clase de selector de directivas predeterminada existente para personalizar comportamientos específicos. |
| `auditude.AuditudeAdProvider` | Obsoleto. Utilice AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Clase que gestiona la resolución de anuncios en horario estelar en el proceso Frase. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Clase que implementa la interfaz ContentTracker y define los eventos de seguimiento de anuncios Primetime. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Clase que gestiona la parte de resolución de publicidad en el proceso Frase. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interfaz que define el protocolo que debe implementar si desea crear un módulo de seguimiento de anuncios diseñado para integrarse con la biblioteca o un rastreador de anuncios personalizado. Esta interfaz requiere que defina la forma en que se informan los eventos de progreso de publicidad al sistema de seguimiento de anuncios remoto. |
| [Información de ubicación](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Clase que abstrae una solicitud de información de colocación. Cada publicidad resuelta debe tener una información de colocación adjunta. La información de colocación describe dónde se va a colocar la publicidad en la línea de tiempo. Contiene información como: <ul><li>Posición de colocación (en ms) </li><li>Tipo de colocación (previo, medio rollo o posterior) </li><li>Duración del fragmento de contenido principal que se va a reemplazar</li></ul> |
