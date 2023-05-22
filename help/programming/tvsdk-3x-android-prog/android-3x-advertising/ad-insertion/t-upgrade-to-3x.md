---
description: La interfaz com.adobe.mediacore.timeline.TimelineMarker ahora contiene un nuevo método
title: Actualización de la resolución de anuncios diferidos 2.5.x a la resolución de anuncios diferidos 3.0.0 (cambios de API/flujo de trabajo)
exl-id: 403ccb25-99a9-4545-9d17-3b71583bc6d8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Actualización de la resolución de anuncios diferidos 2.5.x a la resolución de anuncios diferidos 3.x (cambios de API/flujo de trabajo):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

La interfaz com.adobe.mediacore.timeline.TimelineMarker ahora contiene un nuevo método:

**Placement.Type getPlacementType()**

Este método devolverá un tipo de posición de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Si una pausa publicitaria no se ha resuelto, la variable `getDuration()`en la interfaz TimelineMarker devolverá 0.

>[!NOTE]
>
>Esta interfaz no siempre se convierte en el tipo com.mediacore.timeline.advertising.AdBreakTimelineItem si aún no se ha resuelto. Será capaz de ser fundido si el `getDuration()` del TimelineMarker es bueno que 0.

**Cambios de eventos:**

`kEventAdResolutionComplete` ahora se deprecia y se activa inmediatamente después de que el reproductor entre en el estado PREPARADO. Las aplicaciones que anteriormente solo escuchaban este evento para dibujar la barra de desplazamiento deben cambiar esto para escucharlo `kEventTimelineUpdated` solo. Una vez resueltas las pausas publicitarias individuales, se crea un nuevo `kEventTimelineUpdated` evento que se enviará.
