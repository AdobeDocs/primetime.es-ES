---
description: La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD), para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de publicidad. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.
title: Inserción de anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Información general {#insert-ads-overview}

La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD), para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de publicidad. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.

Una pausa publicitaria contiene uno o más anuncios que se reproducen en secuencia. TVSDK inserta anuncios en el contenido principal como miembros de una o más pausas publicitarias.

>[!TIP]
>
>Si el anuncio tiene errores, TVSDK ignora el anuncio.
