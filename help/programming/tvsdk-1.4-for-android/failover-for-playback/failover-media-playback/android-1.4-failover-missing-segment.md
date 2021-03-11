---
description: Cuando falta un segmento, por ejemplo cuando un segmento en particular no se descarga, intenta recuperarse mediante una variedad de intentos de conmutación por error. Si no puede recuperarse, genera un error.
title: Falta la conmutación por error de segmento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Faltan conmutación por error de segmento{#missing-segment-failover}

Cuando falta un segmento, por ejemplo cuando un segmento en particular no se descarga, intenta recuperarse mediante una variedad de intentos de conmutación por error. Si no puede recuperarse, genera un error.

Si falta un segmento en el servidor porque, por ejemplo, el archivo de manifiesto no está presente, el segmento no se puede descargar, etc., TVSDK intenta conmutarlo probando las siguientes opciones:

1. Intente realizar una conmutación por error en el mismo segmento, a la misma velocidad de bits, en un archivo de variante.
1. Cambie a una velocidad de bits alternativa (conmutador ABR) en el mismo archivo.
1. Recorra todas las tasas de bits disponibles en cada variante disponible.
1. Omita el segmento y emita una advertencia.

Cuando TVSDK no puede obtener un segmento alternativo, déclencheur una notificación de error `CONTENT_ERROR`. Esta notificación contiene una notificación interna con el código `DOWNLOAD_ERROR` . Si el flujo con el problema es una pista de audio alternativa, genera la notificación de error `AUDIO_TRACK_ERROR`.

Si el motor de vídeo no puede obtener segmentos de forma continua, limita los saltos de segmento continuos a 5, tras los cuales se detiene la reproducción y emite un `NATIVE_ERROR` con el código 5.

>[!NOTE]
>
>Los parámetros de control de velocidad de bits adaptable (ABR) no se tienen en cuenta cuando se produce una conmutación por error. Esto se debe a que el mecanismo de conmutación por error está diseñado para usar cualquiera de las listas de reproducción disponibles actualmente, independientemente de su perfil de velocidad de bits, como flujos de backup.
>
>Durante una operación de conmutación por error, puede haber un conmutador de perfil. Si se produce un error durante la descarga de uno de los segmentos de la lista de reproducción, se omiten parámetros de control de ABR como tasa de bits mínima/máxima permitida.

