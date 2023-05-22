---
description: Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning.
title: Requisitos publicitarios
exl-id: 164a5e79-1634-4853-a2b9-d4b5bdbbf190
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Requisitos publicitarios {#advertising-requirements}

Puede insertar anuncios en su VOD y contenido en directo/lineal mediante la interfaz de Adobe Primetime ad decisioning.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetime ad Decisioning funciona con TVSDK para identificar oportunidades de publicidad, resolver anuncios e insertar anuncios resueltos en sus flujos de vídeo.

Para incorporar anuncios al contenido del vídeo, asegúrese de que la publicidad y el contenido del vídeo principal cumplan los siguientes requisitos:

* La versión HLS del contenido publicitario no puede ser superior a la versión HLS del contenido principal.
* Los anuncios deben ser multiplexados y contener una representación de solo audio, independientemente de si el contenido principal es multiplexado.
* Las listas de reproducción de anuncios deben tener las mismas representaciones de velocidad de bits que las representaciones de la lista de reproducción del contenido principal.
* La duración del objetivo y la duración del fragmento individual de un anuncio no pueden superar la duración del objetivo del contenido principal.
* Si el contenido principal contiene un flujo de solo audio, el contenido de la publicidad también debe contener un flujo de solo audio.
* Si el contenido principal contiene secuencias de subtítulos, el contenido de la publicidad debe estar descifrado.
* Si el contenido principal es de tasa de bits múltiple (MBR), el contenido de la publicidad también debe ser MBR.
* Si el contenido principal tiene pistas de audio alternativas, cada anuncio debe tener al menos una secuencia de solo audio o los anuncios deben ser demuxed. Si el anuncio no tiene al menos un flujo de solo audio ni está demuxado, se omite el anuncio.
