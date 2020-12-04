---
description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-title: Suscripción a etiquetas personalizadas
title: Suscripción a etiquetas personalizadas
uuid: fe8ba34d-66fc-43bb-b98e-659c1702d1e0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# Suscripción a etiquetas personalizadas{#subscribe-to-custom-tags}

TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.

Antes de los inicios de reproducción, debe suscribirse a las etiquetas.
Para recibir notificaciones sobre las etiquetas personalizadas en los manifiestos HLS:

Configure los nombres de etiquetas de publicidad personalizados de forma global pasando una matriz que contenga las etiquetas personalizadas a `setSubscribedTags` en `MediaPlayerItemConfig`.

>[!IMPORTANT]
>
>Debe incluir el prefijo `#` al trabajar con flujos HLS.

Por ejemplo:

```java
String[] array = new String[3]; 
array[0] = "#EXT-X-ASSET"; 
array[1] = "#EXT-X-BLACKOUT"; 
array[2] = "#EXT-OATCLS-SCTE35"; 
MediaPlayerItemConfig.setSubscribedTags(array);
```

