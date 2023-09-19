---
description: Los flujos de medios pueden llevar metadatos adicionales en forma de etiquetas en el archivo de descripción de presentación de medios (MPD), y este archivo indica la colocación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.
title: Etiquetas personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Información general {#custom-tags-overview}

Los flujos de medios pueden llevar metadatos adicionales en forma de etiquetas en el archivo de descripción de presentación de medios (MPD), y este archivo indica la colocación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.

## Etiquetas de contenido HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Esta función no está disponible para Safari en equipos con Apple, ya que TVSDK del explorador utiliza la etiqueta de vídeo, en lugar de Flash o MSE, para reproducir contenido HLS.

El TVSDK del explorador es compatible de serie con etiquetas publicitarias #EXT específicas. La aplicación puede utilizar etiquetas personalizadas para mejorar el flujo de trabajo de la publicidad o para admitir situaciones de interrupción. Para admitir flujos de trabajo avanzados, el TVSDK del explorador le permite especificar y suscribirse a etiquetas adicionales en el manifiesto. Puede recibir una notificación cuando estas etiquetas aparezcan en el archivo de manifiesto.

>[!TIP]
>
>Puede suscribirse a etiquetas personalizadas tanto para VOD como para emisiones en directo/lineales.

>[!NOTE]
>
>Cuando se reproduce HLS con la etiqueta de vídeo en Safari y no con la reserva de Flash, esta función no estará disponible en Safari.

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

* Una notificación cuando `#EXT-X-ASSET` las etiquetas, o cualquier otro conjunto de nombres de etiqueta personalizados a los que se haya suscrito, existen en el archivo.
* Insertar anuncios cuando un `#EXT-X-AD` , o cualquier otro nombre de etiqueta personalizado, se encuentra en el flujo.

Puede suscribirse a cualquiera de las siguientes etiquetas como etiquetas personalizadas: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. Se le notifica con una `TimedMetadata` durante el análisis de los archivos de manifiesto.

Hay algunas etiquetas publicitarias, como `EXT-X-CUE`, a la que ya está suscrito. Estas etiquetas de anuncio también las utiliza el generador de oportunidades predeterminado. Puede especificar qué etiquetas de publicidad utiliza el generador de oportunidades predeterminado estableciendo la variable `adTags` propiedad.

## Etiquetas de contenido de DASH {#section_967A952319BE4048B4C6612FFF7ADA6E}

DASH tiene dos formas de señalización de eventos:

* En el archivo MPD.

  Este archivo es similar al archivo M3U8 del contenido HLS y los eventos MPD existen en el archivo .mpd.
* En banda en la representación

  Los eventos en banda se multiplexan con representaciones agregando los mensajes de evento como parte de los segmentos. Una representación es una lista de segmentos de vídeo y audio que se reproducen en secuencia. Los datos de evento en banda están incrustados en estos segmentos.

Estos eventos se notifican como `TimedMetadata` a la aplicación en cuanto el TVSDK del explorador los analice. Una vez notificado un evento, no se le notificará de nuevo.
