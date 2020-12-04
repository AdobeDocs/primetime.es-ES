---
description: 'La interfaz com.adobe.mediacore.timeline.TimelineMarker ahora contiene un nuevo método '
seo-description: 'La interfaz com.adobe.mediacore.timeline.TimelineMarker ahora contiene un nuevo método '
seo-title: 'Actualización de 2.5.x Lazy Ad Resolving a 3.0.0 Lazy Ad Resolving (cambios de API/flujo de trabajo) '
title: 'Actualización de 2.5.x Lazy Ad Resolving a 3.0.0 Lazy Ad Resolving (cambios de API/flujo de trabajo) '
uuid: 5870ceb4-93a8-4c8b-b716-673396122644
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Actualización de 2.5.x Lazy Ad Resolving a 3.x Lazy Ad Resolving (cambios de API/flujo de trabajo):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

La interfaz com.adobe.mediacore.timeline.TimelineMarker ahora contiene un nuevo método:

**Placement.Type getPlacementType()**

Este método devolverá un tipo de colocación de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Si no se resuelve una pausa publicitaria, el método `getDuration()`de la interfaz TimelineMarker devolverá 0.

>[!NOTE]
>
>Esta interfaz no siempre se incluye en el tipo com.mediacore.timeline.publicidad.AdBreakTimelineItem si aún no se ha resuelto. Se podrá convertir si el método `getDuration()` de TimelineMarker es bueno a 0.

**Cambios de evento:**

`kEventAdResolutionComplete` ahora se deprecia y se activa inmediatamente después de que el reproductor entre en el estado PREPARADO. Las aplicaciones que anteriormente solo escuchaban este evento para dibujar la barra de borrado deberían cambiar esto para escuchar sólo `kEventTimelineUpdated`. Una vez resueltas las pausas publicitarias individuales, se enviará un nuevo evento `kEventTimelineUpdated`.
