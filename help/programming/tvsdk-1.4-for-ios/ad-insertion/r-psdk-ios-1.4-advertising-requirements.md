---
title: Requisitos de publicidad
description: Requisitos de publicidad
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Requisitos de publicidad {#advertising-requirements}

Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning .

La toma de decisiones de anuncios de Primetime funciona con TVSDK para identificar oportunidades de publicidad, resolver anuncios e insertar anuncios resueltos en sus flujos de vídeo.

Para incorporar publicidades al contenido del vídeo, asegúrese de que la publicidad y el contenido del vídeo principal cumplan los siguientes requisitos:

* La versión HLS del contenido publicitario no puede ser superior a la versión HLS del contenido principal.
* Los anuncios deben ser multiplexados y contener una representación de solo audio, independientemente de si el contenido principal está multiplexado o no.
* Las listas de reproducción de anuncios deben tener las mismas representaciones de velocidad de bits que las representaciones de la lista de reproducción de contenido principal.
* La duración objetivo y la duración de fragmento individual de un anuncio no pueden superar la duración objetivo del contenido principal.
* Si el contenido principal contiene un flujo de solo audio, el contenido publicitario también debe contener un flujo de solo audio.
* Si el contenido principal contiene secuencias de subtítulos, el contenido publicitario debe estar sin encriptar.
* Si el contenido principal es una tasa de bits múltiple (MBR), el contenido publicitario también debe ser MBR.
* Si el contenido principal tiene pistas de audio alternativas, cada anuncio debe tener al menos un flujo de solo audio.

   Si el anuncio no tiene al menos un flujo de solo audio, se omite el anuncio.