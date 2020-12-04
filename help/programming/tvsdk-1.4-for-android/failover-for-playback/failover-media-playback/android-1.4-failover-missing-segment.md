---
description: Cuando falta un segmento, por ejemplo cuando un segmento en particular no se descarga, intenta recuperarse mediante una serie de intentos de conmutación por error. Si no puede recuperarse, emite un error.
seo-description: Cuando falta un segmento, por ejemplo cuando un segmento en particular no se descarga, intenta recuperarse mediante una serie de intentos de conmutación por error. Si no puede recuperarse, emite un error.
seo-title: Falta la conmutación por error de segmentos
title: Falta la conmutación por error de segmentos
uuid: 17ee1221-e1eb-4f64-a406-4d7eff1d7555
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Falta la conmutación por error de segmentos{#missing-segment-failover}

Cuando falta un segmento, por ejemplo cuando un segmento en particular no se descarga, intenta recuperarse mediante una serie de intentos de conmutación por error. Si no puede recuperarse, emite un error.

Si falta un segmento en el servidor porque, por ejemplo, el archivo de manifiesto no está presente, no se puede descargar el segmento, etc., TVSDK intenta conmutarlo probando las siguientes opciones:

1. Intente realizar una conmutación por error en el mismo segmento, a la misma velocidad de bits, en un archivo de variante.
1. Cambie a una velocidad de bits alternativa (conmutador ABR) en el mismo archivo.
1. Recorra cada velocidad de bits disponible en cada variante disponible.
1. Omita el segmento y emite una advertencia.

Cuando TVSDK no puede obtener un segmento alternativo, activa una notificación de error `CONTENT_ERROR`. Esta notificación contiene una notificación interna con el código `DOWNLOAD_ERROR`. Si el flujo con el problema es una pista de audio alternativa, genera la notificación de error `AUDIO_TRACK_ERROR`.

Si el motor de vídeo no puede obtener segmentos de forma continua, limita los saltos de segmento continuos a 5, tras los cuales se detiene la reproducción y emite un `NATIVE_ERROR` con el código 5.

>[!NOTE]
>
>Los parámetros de control de velocidad de bits adaptable (ABR) no se tienen en cuenta cuando se produce una conmutación por error. Esto se debe a que el mecanismo de conmutación por error está diseñado para utilizar como flujos de backup cualquiera de las listas de reproducción disponibles actualmente, independientemente del perfil de velocidad de bits.
>
>Durante una operación de conmutación por error, puede haber un conmutador de perfil. Si se produce un error durante la descarga de uno de los segmentos de la lista de reproducción, se omiten los parámetros de control de ABR, como la velocidad de bits mínima/máxima permitida.

