---
description: La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD), para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de publicidad. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.
title: Inserción de anuncios
exl-id: 899d28b5-92aa-42cb-b7e8-9168fb68dbbd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Información general {#insert-ads-overview}

La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD), para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de publicidad. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.

Un *`ad break`* contiene uno o más anuncios que se reproducen en secuencia. TVSDK inserta anuncios en el contenido principal como miembros de una o más pausas publicitarias.

>[!NOTE]
>
>Si el anuncio tiene errores, TVSDK ignora el anuncio.
