---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-title: Gestión de errores de reemplazo y eliminación de publicidad
title: Gestión de errores de reemplazo y eliminación de publicidad
uuid: 615f42b7-733a-49c4-bd7a-f14ad0d23fa0
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Gestión de errores de reemplazo y eliminación de publicidad {#ad-deletion-and-replacement-error-handling}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.

TVSDK administra `timeRanges` los errores mediante procesos predeterminados de combinación y reordenación. En primer lugar, el reproductor ordena los intervalos de tiempo definidos por el cliente según la hora de *inicio* . En función de este orden de clasificación, si hay subconjuntos e intersecciones entre los intervalos, TVSDK combina los intervalos adyacentes y los une.

TVSDK gestiona los errores de intervalo de tiempo con las siguientes opciones:

* **De forma desordenada** , TVSDK reordena los intervalos de tiempo.

* **El subconjunto** TVSDK combina los subconjuntos de intervalo de tiempo.

* **La intersección** de TVSDK combina los intervalos de tiempo que se intersectan.

* **Reemplazar rangos conflicto** TVSDK selecciona la duración de reemplazo desde la primera `timeRange` que aparece en el grupo en conflicto.

TVSDK gestiona los conflictos de modo de señalización con metadatos de anuncio de las siguientes formas:

* Si el modo de señalización de publicidad entra en conflicto con los metadatos del intervalo de tiempo, los metadatos del intervalo de tiempo siempre tienen prioridad.

   Por ejemplo, si el modo de señalización de publicidad se configura como mapa del servidor o como señales de manifiesto, y también hay rangos de tiempo MARK en los metadatos de publicidad, el comportamiento resultante es que los rangos están marcados y no se insertan anuncios.
* Para los intervalos REPLACE, si el modo de señalización está establecido como mapa del servidor o señales de manifiesto, los intervalos se reemplazan como se especifica en los rangos REPLACE y no hay inserción de anuncios a través de mapas del servidor o señales de manifiesto.

   Para obtener más información, consulte la tabla *Modo de señalización / Comportamientos* de combinación de metadatos en [Efecto en la inserción y eliminación de anuncios del modo](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md)de señalización de publicidad.

Recuerde lo siguiente:

* Cuando el servidor no devuelve un valor válido `AdBreaks`, TVSDK genera y procesa un valor `NOPTimelineOperation` para AdBreak vacío y no se reproduce ningún anuncio.

* Aunque la eliminación/sustitución de anuncios C3 está pensada para que solo sea compatible con VOD, si se especifica en los metadatos de la publicidad, los intervalos de tiempo también se procesan para flujos en vivo.
