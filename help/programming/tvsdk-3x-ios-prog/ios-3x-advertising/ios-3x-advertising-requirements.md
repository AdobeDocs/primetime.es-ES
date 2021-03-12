---
description: Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning .
title: Requisitos de publicidad
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Requisitos de publicidad {#advertising-requirements}

Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning .

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

La toma de decisiones de anuncios de Primetime funciona con TVSDK para identificar oportunidades de publicidad, resolver anuncios e insertar anuncios resueltos en sus flujos de vídeo.

Para incorporar publicidades al contenido del vídeo, asegúrese de que la publicidad y el contenido del vídeo principal cumplan los siguientes requisitos:

* La versión HLS del contenido publicitario no puede ser superior a la versión HLS del contenido principal.
* Los anuncios deben ser multiplexados y contener una representación de solo audio, independientemente de si el contenido principal está multiplexado o no.
* Las listas de reproducción de anuncios deben tener las mismas representaciones de velocidad de bits que las representaciones de la lista de reproducción de contenido principal.
* La duración objetivo y la duración de fragmento individual de un anuncio no pueden superar la duración objetivo del contenido principal.
* Si el contenido principal contiene un flujo de solo audio, el contenido publicitario también debe contener un flujo de solo audio.
* Si el contenido principal contiene secuencias de subtítulos, el contenido publicitario debe estar sin encriptar.
* Si el contenido principal es una tasa de bits múltiple (MBR), el contenido publicitario también debe ser MBR.
* Si el contenido principal tiene pistas de audio alternativas, cada anuncio debe tener al menos un flujo de solo audio o los anuncios deben ser desactivados. Si el anuncio no tiene al menos un flujo de solo audio ni está desactivado, se omite el anuncio.