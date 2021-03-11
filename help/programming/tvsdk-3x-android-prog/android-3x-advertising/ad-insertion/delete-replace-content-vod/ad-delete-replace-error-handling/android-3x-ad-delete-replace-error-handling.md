---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.
title: Gestión de errores de reemplazo y eliminación de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Administración de errores de eliminación y reemplazo de publicidad {#ad-deletion-and-replacement-error-handling}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.

TVSDK administra los errores `timeRanges` mediante procesos de combinación y reordenación predeterminados. En primer lugar, el reproductor ordena los intervalos de tiempo definidos por el cliente por la *hora de inicio*. En función de este orden de clasificación, si hay subconjuntos e intersecciones entre los intervalos, TVSDK combina intervalos adyacentes y los une.

TVSDK gestiona los errores de intervalo de tiempo con las siguientes opciones:

* **Fuera de** ordenTVSDK reordena los intervalos de tiempo.

* **** SubsetTVSDK combina los subconjuntos de intervalo de tiempo.

* **** IntersectionTVSDK combina los intervalos de tiempo que se intersectan.

* **Reemplazar rangos** conflictTVSDK selecciona la duración de reemplazo de la más temprana  `timeRange` que aparezca en el grupo en conflicto.

TVSDK gestiona los conflictos del modo de señalización con los metadatos de publicidad de las siguientes maneras:

* Si el modo de señalización de anuncio entra en conflicto con los metadatos del intervalo de tiempo, estos siempre tienen prioridad.

   Por ejemplo, si el modo de señalización de publicidad está establecido como mapa del servidor o señal de manifiesto y también hay intervalos de tiempo MARK en los metadatos de publicidad, el comportamiento resultante es que los intervalos están marcados y no se insertan anuncios.
* En los intervalos REPLACE, si el modo de señalización está definido como mapa del servidor o como señales de manifiesto, los intervalos se sustituyen según se especifica en los intervalos REPLACE y no hay inserción de anuncios a través del mapa del servidor o las indicaciones de manifiesto.

   Para obtener más información, consulte la tabla *Signaling Mode / Metadata Combination Behaviors* en [Effect on ad insertion and delete from ad signal mode](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md).

Recuerde lo siguiente:

* Cuando el servidor no devuelve un valor `AdBreaks` válido, TVSDK genera y procesa un valor `NOPTimelineOperation` para el AdBreak vacío y no se reproduce ningún anuncio.

* Aunque la eliminación/sustitución de anuncios C3 está pensada para que solo sea compatible con VOD, si se especifica en los metadatos de los anuncios, también se procesan intervalos de tiempo para emisiones en directo.
