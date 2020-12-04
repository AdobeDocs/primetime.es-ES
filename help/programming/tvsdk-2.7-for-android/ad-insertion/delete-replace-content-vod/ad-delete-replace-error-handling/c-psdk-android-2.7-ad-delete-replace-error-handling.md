---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-title: Gestión de errores de reemplazo y eliminación de publicidad
title: Gestión de errores de reemplazo y eliminación de publicidad
uuid: 9a951bc4-b372-4655-8510-3f474171415d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Información general {#ad-deletion-and-replacement-error-handling-overview}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico combinando o reordenando los intervalos de tiempo incorrectamente definidos.

TVSDK administra `timeRanges` errores mediante procesos predeterminados de combinación y reordenación. En primer lugar, el reproductor ordena los intervalos de tiempo definidos por el cliente por la hora *de inicio*. En función de este orden de clasificación, si hay subconjuntos e intersecciones entre los intervalos, TVSDK combina los intervalos adyacentes y los une.

TVSDK gestiona los errores de intervalo de tiempo con las siguientes opciones:

* **Fuera de** ordenTVSDK reordena los intervalos de tiempo.

* **** SubsetTVSDK combina los subconjuntos de intervalo de tiempo.

* **** IntersectTVSDK combina los intervalos de tiempo interrelacionados.

* **Reemplazar intervalos** conflictoTVSDK selecciona la duración de reemplazo desde la primera  `timeRange` que aparece en el grupo en conflicto.

TVSDK gestiona los conflictos de modo de señalización con metadatos de anuncio de las siguientes formas:

* Si el modo de señalización de publicidad entra en conflicto con los metadatos del intervalo de tiempo, los metadatos del intervalo de tiempo siempre tienen prioridad.

   Por ejemplo, si el modo de señalización de publicidad se configura como mapa del servidor o como señales de manifiesto, y también hay rangos de tiempo MARK en los metadatos de publicidad, el comportamiento resultante es que los rangos están marcados y no se insertan anuncios.
* Para los intervalos REPLACE, si el modo de señalización está establecido como mapa del servidor o señales de manifiesto, los intervalos se reemplazan como se especifica en los rangos REPLACE y no hay inserción de anuncios a través de mapas del servidor o señales de manifiesto.

   Para obtener más información, consulte la tabla *Comportamientos de combinación de metadatos / Modo de señalización* en [Efecto en la inserción y eliminación de publicidades del modo de señalización de publicidad...](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

Recuerde lo siguiente:

* Cuando el servidor no devuelve un `AdBreaks` válido, TVSDK genera y procesa un `NOPTimelineOperation` para el AdBreak vacío y no se reproduce ningún anuncio.

* Aunque la eliminación/sustitución de anuncios C3 está pensada para que solo sea compatible con VOD, si se especifica en los metadatos de la publicidad, los intervalos de tiempo también se procesan para flujos en vivo.

