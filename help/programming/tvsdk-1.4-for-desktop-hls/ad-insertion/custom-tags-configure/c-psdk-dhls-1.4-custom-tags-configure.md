---
description: Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto, y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.
title: Etiquetas personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Etiquetas personalizadas{#custom-tags}

Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto, y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.

## Etiquetas de contenido HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Esta función no está disponible para Safari en equipos Apple, ya que TVSDK utiliza la etiqueta de vídeo, en lugar de Flash o MSE, para reproducir contenido HLS.

TVSDK proporciona compatibilidad predeterminada con etiquetas publicitarias #EXT específicas. La aplicación puede utilizar etiquetas personalizadas para mejorar el flujo de trabajo publicitario o para admitir situaciones de bloqueo. Para admitir flujos de trabajo avanzados, TVSDK permite especificar y suscribirse a etiquetas adicionales en el manifiesto. Se le puede notificar cuando estas etiquetas aparezcan en el archivo de manifiesto.

>[!TIP]
>
>Puede suscribirse a etiquetas personalizadas tanto para VOD como para flujos en directo/lineales.

>[!NOTE]
>
>Cuando se reproduce HLS utilizando la etiqueta de vídeo en Safari y no utilizando la reserva de Flash, esta función no estará disponible en Safari.

## Uso de etiquetas HLS personalizadas {#section_AD032318AEF5418393D2B1DF36B0BABB}

Este es un ejemplo de recurso de VOD personalizado:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

La aplicación puede configurar los siguientes escenarios:

* En el archivo existe una notificación cuando `#EXT-X-ASSET` etiquetas, o cualquier otro conjunto de nombres de etiquetas personalizados al que se haya suscrito.
* Inserte publicidades cuando se encuentre una etiqueta `#EXT-X-AD` o cualquier otro nombre de etiqueta personalizado en el flujo.

Puede suscribirse a cualquiera de las siguientes etiquetas como etiquetas personalizadas: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. Se le notifica con un evento `TimedMetadata` durante el análisis de los archivos de manifiesto.

Hay algunas etiquetas publicitarias, como `EXT-X-CUE`, a las que ya está suscrito. El generador de oportunidades predeterminado también utiliza estas etiquetas de publicidad. Puede especificar qué etiquetas de publicidad utiliza el generador de oportunidades predeterminado estableciendo la propiedad `adTags` .
