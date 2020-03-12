---
description: Puede insertar anuncios en el VOD y contenido en directo o lineal mediante la interfaz de toma de decisiones de anuncios de Adobe Primetime.
seo-description: Puede insertar anuncios en el VOD y contenido en directo o lineal mediante la interfaz de toma de decisiones de anuncios de Adobe Primetime.
seo-title: Requisitos de publicidad
title: Requisitos de publicidad
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Requisitos de publicidad {#advertising-requirements}

Puede insertar anuncios en el VOD y contenido en directo o lineal mediante la interfaz de toma de decisiones de anuncios de Adobe Primetime.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetime y la toma de decisiones funciona con TVSDK para identificar oportunidades de publicidad, resolver publicidades e insertar publicidades resueltas en sus flujos de vídeo.

Para incorporar publicidades en el contenido de vídeo, asegúrese de que la publicidad y el contenido de vídeo principal cumplen los siguientes requisitos:

* La versión HLS del contenido de publicidad no puede ser superior a la versión HLS del contenido principal.
* Las publicidades deben ser multiplexadas y contener una representación solo de audio, independientemente de si el contenido principal está multiplexado.
* Las listas de reproducción de anuncios deben tener las mismas representaciones de velocidad de bits que las representaciones de la lista de reproducción de contenido principal.
* La duración objetivo y la duración del fragmento individual de una publicidad no pueden superar la duración objetivo del contenido principal.
* Si el contenido principal contiene un flujo de solo audio, el contenido de la publicidad también debe contener un flujo de solo audio.
* Si el contenido principal contiene flujos de subtítulos, el contenido de la publicidad debe estar sin cifrar.
* Si el contenido principal es una velocidad de bits múltiple (MBR), el contenido de la publicidad también debe ser MBR.
* Si el contenido principal tiene pistas de audio alternativas, cada anuncio debe tener al menos un flujo de solo audio.

Si la publicidad no tiene al menos un flujo de solo audio, se omitirá.