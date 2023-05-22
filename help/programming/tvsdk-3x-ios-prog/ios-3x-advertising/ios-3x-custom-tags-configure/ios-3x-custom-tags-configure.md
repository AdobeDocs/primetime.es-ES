---
description: Los flujos de medios pueden llevar metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto, y este archivo indica la colocación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.
title: Etiquetas personalizadas
exl-id: 4518904a-6f85-403b-b819-004e3e1cbb96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Información general {#custom-tags-overview}

Los flujos de medios pueden llevar metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto, y este archivo indica la colocación de la publicidad. Puede especificar nombres de etiquetas personalizados y recibir notificaciones cuando determinadas etiquetas aparezcan en el archivo de manifiesto.

## Etiquetas de contenido HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Esta función no está disponible para Safari en equipos Apple, ya que TVSDK utiliza la etiqueta de vídeo, en lugar de Flash o MSE, para reproducir contenido HLS.

TVSDK es compatible de serie con etiquetas de publicidad #EXT específicas. La aplicación puede utilizar etiquetas personalizadas para mejorar el flujo de trabajo de la publicidad o para admitir situaciones de interrupción. Para admitir flujos de trabajo avanzados, TVSDK permite especificar y suscribirse a etiquetas adicionales en el manifiesto. Puede recibir una notificación cuando estas etiquetas aparezcan en el archivo de manifiesto.

>[!TIP]
>
>Puede suscribirse a etiquetas personalizadas tanto para VOD como para emisiones en directo/lineales.

>[!NOTE]
>
>Cuando se reproduce HLS con la etiqueta de vídeo en Safari y no con la reserva de Flash, esta función no estará disponible en Safari.

## Usar etiquetas HLS personalizadas {#section_AD032318AEF5418393D2B1DF36B0BABB}

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
