---
description: 'La interfaz com.adobe.mediacore.cronología.TimelineMarker ahora contiene un nuevo método '
title: 'Actualización de 2.5.x Lazy Ad Resolving a 3.0.0 Lazy Ad Resolving (cambios en API/flujo de trabajo) '
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Actualización de la resolución de publicidad diferida 2.5.x a la resolución de publicidad diferida 3.x (cambios en la API/flujo de trabajo):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

La interfaz com.adobe.mediacore.línea de tiempo.TimelineMarker ahora contiene un nuevo método:

**Placement.Type getPlacementType()**

Este método devolverá un tipo de colocación de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Si no se resuelve una pausa publicitaria, el método `getDuration()`de la interfaz TimelineMarker devolverá 0.

>[!NOTE]
>
>Esta interfaz no siempre se incluye en el tipo com.mediacore.línea de tiempo.advertising.AdBreakTimelineItem si aún no se ha resuelto. Se puede convertir si el método `getDuration()` de TimelineMarker es bueno a 0.

**Cambios de eventos:**

`kEventAdResolutionComplete` ahora se deprecia y ahora se activa inmediatamente después de que el reproductor entre en el estado PREPARADO . Las aplicaciones que anteriormente solo escuchaban este evento para dibujar la barra de depuración deben cambiar esto para escuchar solo `kEventTimelineUpdated`. Una vez resueltas las pausas publicitarias individuales, se enviará un nuevo evento `kEventTimelineUpdated`.
