---
description: La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD), para flujo continuo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido por fases.
title: Insertar publicidades
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Información general {#insert-ads-overview}

La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD), para flujo continuo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido por fases.

Un *`ad break`* contiene uno o más anuncios que se reproducen en secuencia. TVSDK inserta anuncios en el contenido principal como miembros de una o más pausas publicitarias.

>[!NOTE]
>
>Si el anuncio tiene errores, TVSDK ignora el anuncio.