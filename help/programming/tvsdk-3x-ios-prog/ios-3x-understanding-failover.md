---
description: La administración de la conmutación por error se produce cuando una lista de reproducción de variante tiene varias representaciones para la misma velocidad de bits y una de las representaciones deja de funcionar. El TVSDK cambia entre representaciones.
seo-description: La administración de la conmutación por error se produce cuando una lista de reproducción de variante tiene varias representaciones para la misma velocidad de bits y una de las representaciones deja de funcionar. El TVSDK cambia entre representaciones.
seo-title: Conmutación por error
title: Conmutación por error
uuid: 064886ab-afa2-4afc-b795-d094b31934b8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Failover {#failover}

La administración de la conmutación por error se produce cuando una lista de reproducción de variante tiene varias representaciones para la misma velocidad de bits y una de las representaciones deja de funcionar. El TVSDK cambia entre representaciones.

El siguiente ejemplo muestra una lista de reproducción de variante con direcciones URL de conmutación por error con la misma velocidad de bits:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Cuando TVSDK carga la lista de reproducción de variante, crea una cola que contiene las direcciones URL de todas las representaciones del contenido para la misma velocidad de bits. Cuando falla una solicitud de URL, TVSDK utiliza la siguiente URL de la misma velocidad de bits de la cola de conmutación por error. En cualquier momento de error específico, TVSDK pasa una vez por todas las direcciones URL disponibles hasta encontrar una que funcione correctamente o hasta que haya intentado todas las direcciones URL disponibles. Si TVSDK ha intentado acceder a todas las direcciones URL disponibles y ninguna de ellas funciona, TVSDK deja de intentar reproducir el contenido.

La conmutación por error solo se produce en el nivel M3U8, lo que significa:

* En el caso de VOD, la conmutación por error solo puede producirse cuando comienza a intentar reproducirse y no después de que se ha empezado a reproducir.
* Para el flujo en directo, la conmutación por error puede ocurrir en medio del flujo.

>[!TIP]
>
>TVSDK, en lugar del reproductor Apple AV Foundation, proporciona la gestión de conmutación por error.