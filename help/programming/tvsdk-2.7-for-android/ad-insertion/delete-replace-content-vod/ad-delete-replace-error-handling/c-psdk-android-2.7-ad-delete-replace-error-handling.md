---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo definidos incorrectamente.
title: Gestión de errores de eliminación y sustitución de anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Información general {#ad-deletion-and-replacement-error-handling-overview}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo definidos incorrectamente.

TVSDK administra `timeRanges` errores mediante los procesos de combinación y reordenación predeterminados. En primer lugar, el reproductor ordena los intervalos de tiempo definidos por el cliente según el *comenzar* hora. En función de este orden de clasificación, si hay subconjuntos e intersecciones entre los intervalos, TVSDK combina intervalos adyacentes y combina estos intervalos.

TVSDK gestiona los errores de intervalo de tiempo con las siguientes opciones:

* **Fuera de servicio** TVSDK reordena los intervalos de tiempo.

* **Subconjunto** TVSDK combina los subconjuntos de intervalo de tiempo.

* **Intersect** TVSDK combina los intervalos de tiempo de intersección.

* **Conflicto de intervalos de reemplazo** TVSDK selecciona la duración de reemplazo de la primera `timeRange` que aparece en el grupo en conflicto.

TVSDK controla los conflictos del modo de señalización con los metadatos de publicidad de las siguientes maneras:

* Si el modo de señalización de publicidad entra en conflicto con los metadatos de intervalo de tiempo, estos siempre tienen prioridad.

  Por ejemplo, si el modo de señalización de publicidad se establece como mapa del servidor o señales de manifiesto y también hay intervalos de tiempo MARK en los metadatos de publicidad, el comportamiento resultante es que los intervalos se marcan y no se insertan anuncios.
* En el caso de los intervalos REPLACE, si el modo de señalización está configurado como mapa del servidor o señales de manifiesto, los intervalos se sustituyen como se especifica en los intervalos REPLACE y no hay inserción de anuncios a través de las señales de mapa del servidor o de manifiesto.

  Para obtener más información, consulte la *Comportamientos de combinación de metadatos/modo de señalización* tabla en [Efecto en la inserción y eliminación de anuncios desde el modo de señalización de anuncios...](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

Recuerde lo siguiente:

* Cuando el servidor no devuelve datos válidos `AdBreaks`, TVSDK genera y procesa un `NOPTimelineOperation` para el AdBreak vacío y no se reproduce ningún anuncio.

* Aunque la eliminación/sustitución de anuncios C3 está pensada para ser compatible únicamente con VOD, si se especifica en los metadatos de la publicidad, los intervalos de tiempo también se procesan para emisiones en directo.
