---
description: La administración de la conmutación por error se produce cuando una lista de reproducción de variante tiene varias representaciones para la misma velocidad de bits y una de las representaciones deja de funcionar. TVSDK cambia entre representaciones.
title: Failover
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Failover {#failover}

La administración de la conmutación por error se produce cuando una lista de reproducción de variante tiene varias representaciones para la misma velocidad de bits y una de las representaciones deja de funcionar. TVSDK cambia entre representaciones.

El siguiente ejemplo muestra una lista de reproducción de variante con direcciones URL de conmutación por error con la misma velocidad de bits:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Cuando TVSDK carga la lista de reproducción de variante, crea una cola que contiene las URL de todas las representaciones del contenido para la misma velocidad de bits. Cuando falla una solicitud de una URL, TVSDK utiliza la siguiente URL con la misma velocidad de bits de la cola de conmutación por error. En cualquier momento de error específico, TVSDK recorre una vez todas las direcciones URL disponibles hasta encontrar una que funcione correctamente o hasta que haya intentado todas las direcciones URL disponibles. Si TVSDK ha intentado recuperar todas las URL disponibles y ninguna de ellas funciona, TVSDK deja de intentar reproducir el contenido.

La conmutación por error solo se produce en el nivel M3U8, lo que significa que:

* Para VOD, la conmutación por error solo se puede producir cuando comienza a intentar reproducirse y no después de que haya comenzado a reproducirse.
* Para el streaming en vivo, la conmutación por error puede ocurrir en medio del flujo.

>[!TIP]
>
>TVSDK, en lugar del reproductor Apple AV Foundation, proporciona administración de conmutación por error.
