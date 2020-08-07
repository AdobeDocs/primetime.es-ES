---
description: Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto, y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.
seo-description: Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto, y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.
seo-title: Etiquetas personalizadas
title: Etiquetas personalizadas
uuid: a86753ac-23d0-4c5e-9b5c-a6cdb7fcc5f7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Información general {#custom-tags-overview}

Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto, y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.

## Etiquetas de contenido HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Esta función no está disponible para Safari en equipos Apple, ya que TVSDK utiliza la etiqueta de vídeo, en lugar de Flash o MSE, para reproducir contenido HLS.

TVSDK proporciona compatibilidad lista para usar con etiquetas `#EXT` publicitarias específicas. La aplicación puede utilizar etiquetas personalizadas para mejorar el flujo de trabajo de la publicidad o para admitir situaciones de bloqueo. Para admitir flujos de trabajo avanzados, TVSDK permite especificar y suscribirse a etiquetas adicionales en el manifiesto. Puede recibir una notificación cuando estas etiquetas aparezcan en el archivo de manifiesto.

>[!TIP]
>
>Puede suscribirse a etiquetas personalizadas tanto para VOD como para flujos en directo/lineales.

>[!NOTE]
>
>Cuando se reproduce HLS con la etiqueta Vídeo en Safari y no con Flash Fallback, esta función no estará disponible en Safari.

## Uso de etiquetas HLS personalizadas {#section_AD032318AEF5418393D2B1DF36B0BABB}

A continuación se muestra un ejemplo de un recurso de VOD personalizado:

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

* Una notificación cuando `#EXT-X-ASSET` las etiquetas, o cualquier otro conjunto de nombres de etiquetas personalizados al que se haya suscrito, existan en el archivo.
* Inserte publicidades cuando se encuentre una `#EXT-X-AD` etiqueta o cualquier otro nombre de etiqueta personalizado en el flujo.

Puede suscribirse a cualquiera de las etiquetas siguientes como etiquetas personalizadas:

* `EXT-PROGRAM-DATE-TIME`
* `EXT-X-START`
* `EXT-X-AD`
* `EXT-X-CUE`
* `EXT-X-ENDLIST`

Se le notificará con un `TimedMetadata` evento durante el análisis de los archivos de manifiesto.

Hay algunas etiquetas de publicidad, como `EXT-X-CUE`la que ya está suscrito. Estas etiquetas de publicidad también se utilizan en el generador de oportunidades predeterminado. Puede especificar qué etiquetas de publicidad utiliza el generador de oportunidades predeterminado si establece la `adTags` propiedad.
