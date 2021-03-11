---
description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.
title: Suscripción a etiquetas personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Suscripción a etiquetas personalizadas{#subscribe-to-custom-tags}

TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.

Antes de iniciar la reproducción, debe suscribirse a las etiquetas .
Para recibir notificaciones sobre etiquetas personalizadas en manifiestos HLS:

Establezca los nombres de etiquetas de publicidad personalizados de forma global pasando una matriz que contenga las etiquetas personalizadas a `setSubscribedTags` en `MediaPlayerItemConfig`.

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

