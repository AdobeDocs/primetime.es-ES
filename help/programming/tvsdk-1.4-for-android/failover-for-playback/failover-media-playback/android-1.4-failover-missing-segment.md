---
description: Cuando falta un segmento, por ejemplo cuando un segmento en particular no se puede descargar, intenta recuperarse mediante varios intentos de conmutación por error. Si no se puede recuperar, genera un error.
title: Falta conmutación por error de segmento
exl-id: e941008a-99a5-4fff-ac88-133abcf9380d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Falta conmutación por error de segmento{#missing-segment-failover}

Cuando falta un segmento, por ejemplo cuando un segmento en particular no se puede descargar, intenta recuperarse mediante varios intentos de conmutación por error. Si no se puede recuperar, genera un error.

Si falta un segmento en el servidor porque, por ejemplo, el archivo de manifiesto no está presente, el segmento no se puede descargar, etc., TVSDK intenta conmutar por error al intentar las siguientes opciones:

1. Intentar una conmutación por error al mismo segmento, a la misma velocidad de bits, en un archivo de variante.
1. Cambie a una velocidad de bits alternativa (conmutador ABR) en el mismo archivo.
1. Pasa por cada velocidad de bits disponible en cada variante disponible.
1. Omita el segmento y emita una advertencia.

Cuando TVSDK no puede obtener un segmento alternativo, déclencheur un `CONTENT_ERROR` notificación de error. Esta notificación contiene una notificación interna con el código `DOWNLOAD_ERROR` código. Si el flujo con el problema es una pista de audio alternativa, genera el `AUDIO_TRACK_ERROR` notificación de error.

Si el motor de vídeo no puede obtener segmentos de forma continua, limita el salto de segmentos continuo a 5, tras lo cual se detiene la reproducción y emite un `NATIVE_ERROR` con el código 5.

>[!NOTE]
>
>Los parámetros de control de velocidad de bits adaptable (ABR) no se tienen en cuenta cuando se produce una conmutación por error. Esto se debe a que el mecanismo de conmutación por error está diseñado para utilizar cualquiera de las listas de reproducción disponibles actualmente, independientemente de su perfil de velocidad de bits, como flujos de copia de seguridad.
>
>Durante una operación de conmutación por error, puede haber un conmutador de perfil. Si se produce un error durante la descarga de uno de los segmentos de la lista de reproducción, se omiten los parámetros de control ABR como la velocidad de bits mínima/máxima permitida.
