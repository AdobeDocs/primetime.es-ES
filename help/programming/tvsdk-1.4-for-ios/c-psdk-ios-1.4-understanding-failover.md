---
description: La administración de la conmutación por error se produce cuando una lista de reproducción de variante tiene varias representaciones para la misma velocidad de bits y una de las representaciones deja de funcionar. El TVSDK cambia entre representaciones.
title: Failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Failover{#failover}

La administración de la conmutación por error se produce cuando una lista de reproducción de variante tiene varias representaciones para la misma velocidad de bits y una de las representaciones deja de funcionar. El TVSDK cambia entre representaciones.

El siguiente ejemplo muestra una lista de reproducción de variante con direcciones URL de conmutación por error con la misma velocidad de bits:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Cuando TVSDK carga la lista de reproducción de variantes, crea una cola que contiene las direcciones URL de todas las representaciones del contenido para la misma velocidad de bits. Cuando falla una solicitud de URL, TVSDK utiliza la siguiente URL de la misma velocidad de bits de la cola de conmutación por error. En cualquier momento de error específico, TVSDK pasa una vez por todas las direcciones URL disponibles hasta que encuentra una que funciona correctamente o hasta que ha intentado todas las direcciones URL disponibles. Si TVSDK ha intentado todas las URL disponibles y ninguna de ellas funciona, TVSDK deja de intentar reproducir el contenido.

La conmutación por error solo se produce en el nivel M3U8, lo que significa:

* Para VOD, la conmutación por error solo puede ocurrir cuando comienza a intentar reproducir y no después de que haya empezado a reproducirse.
* Para la transmisión en vivo, la conmutación por error puede ocurrir en medio del flujo.

>[!TIP]
>
>TVSDK, en lugar del reproductor Apple AV Foundation, proporciona gestión de conmutación por error.

