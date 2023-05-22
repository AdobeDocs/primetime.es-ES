---
description: Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning.
title: Publicidad
exl-id: 79ee4abf-a3f5-4915-ad4b-fe866acec882
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Publicidad y sus requisitos {#advertising-requirements}

Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning.

Primetime ad decisioning funciona con TVSDK para identificar oportunidades de publicidad, resolver anuncios e insertar anuncios resueltos en sus flujos de vídeo.

Para incorporar anuncios al contenido del vídeo, asegúrese de que la publicidad y el contenido del vídeo principal cumplan los siguientes requisitos:

* La versión HLS del contenido publicitario no puede ser superior a la versión HLS del contenido principal.
* Los anuncios no tienen que ser multiplexados (sin restricciones), independientemente de si el contenido principal es multiplexado.
