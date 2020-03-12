---
description: Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de descripción de la presentación de medios (MPD), y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.
seo-description: Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de descripción de la presentación de medios (MPD), y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.
seo-title: Etiquetas personalizadas
title: Etiquetas personalizadas
uuid: d1e34288-545b-440f-a262-2fb853f0e3c4
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Información general {#custom-tags-overview}

Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de descripción de la presentación de medios (MPD), y este archivo indica la ubicación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.

## Etiquetas de contenido HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Esta función no está disponible para Safari en equipos Apple, ya que el SDK del explorador utiliza la etiqueta de vídeo, en lugar de Flash o MSE, para reproducir contenido HLS.

El SDK de TVSDK del explorador proporciona compatibilidad lista para usar con etiquetas de publicidad #EXT específicas. La aplicación puede utilizar etiquetas personalizadas para mejorar el flujo de trabajo de la publicidad o para admitir situaciones de bloqueo. Para admitir flujos de trabajo avanzados, el SDK de TVSDK de explorador le permite especificar y suscribirse a etiquetas adicionales en el manifiesto. Puede recibir una notificación cuando estas etiquetas aparezcan en el archivo de manifiesto.

>[!TIP]
>
>Puede suscribirse a etiquetas personalizadas tanto para VOD como para flujos en directo/lineales.

>[!NOTE] {othertype=&quot;Limitation&quot;}
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

Puede suscribirse a cualquiera de las etiquetas siguientes como etiquetas personalizadas: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`.. Se le notifica con un `TimedMetadata` evento durante el análisis de los archivos de manifiesto.

Hay algunas etiquetas de publicidad, como `EXT-X-CUE`la que ya está suscrito. Estas etiquetas de publicidad también se utilizan en el generador de oportunidades predeterminado. Puede especificar qué etiquetas de publicidad utiliza el generador de oportunidades predeterminado si establece la `adTags` propiedad.

## Etiquetas de contenido DASH {#section_967A952319BE4048B4C6612FFF7ADA6E}

DASH tiene dos formas de señalar eventos:

* En el archivo MPD.

   Este archivo es similar al archivo M3U8 en el contenido HLS y los eventos MPD existen en el archivo .mpd.
* Inband en la representación

   Los eventos dentro de banda se multiplexan con representaciones agregando los mensajes de evento como parte de los segmentos. Una representación es una lista de segmentos de audio y vídeo que se reproducen en secuencia. Los datos del evento de entrada se incrustan en estos segmentos.

Estos eventos se notifican como `TimedMetadata` eventos a la aplicación en cuanto el explorador TVSDK los analiza. Una vez que se notifica un evento, no se le notificará nuevamente.
