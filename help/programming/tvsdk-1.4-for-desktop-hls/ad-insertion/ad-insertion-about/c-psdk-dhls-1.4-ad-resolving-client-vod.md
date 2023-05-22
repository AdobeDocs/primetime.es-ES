---
description: Para el contenido de vídeo bajo demanda (VOD), TVSDK inserta saltos de publicidad uniendo los anuncios en el contenido principal para que aumente la duración de la cronología.
title: Resolución e inserción de anuncios de VOD
exl-id: 6f02c7fc-028d-442f-92d4-9efa671b7f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Resolución e inserción de anuncios de VOD{#vod-ad-resolving-and-insertion}

Para el contenido de vídeo bajo demanda (VOD), TVSDK inserta saltos de publicidad uniendo los anuncios en el contenido principal para que aumente la duración de la cronología.

Antes de la reproducción, TVSDK resuelve los anuncios conocidos, inserta saltos de anuncios en el contenido principal tal como se describe en una cronología devuelta por TVSDK y vuelve a calcular la cronología virtual, si es necesario.

TVSDK inserta anuncios de las siguientes maneras:

* **Pre-roll**, que se encuentra antes del contenido.
* **Mid-roll**, que se encuentra en el contenido.
* **Post-roll**, que va después del contenido.

>[!IMPORTANT]
>
>Al implementar un personalizado `AdPolicySelector`, se puede dar una política diferente a cada tipo de `AdBreakTimelineItem` (pre-roll, mid-roll o post-roll) en `AdPolicyInfo`, según el tipo de `AdBreakTimelineItem`. Por ejemplo, puede mantener el contenido durante la emisión después de que se haya reproducido, pero puede eliminar el contenido previo a la emisión una vez que se haya reproducido.

Después de que comience la reproducción, no se pueden producir cambios adicionales en el contenido. Los anuncios no pueden:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar anuncios integrados del contenido para ofrecer una experiencia sin anuncios.
* Reemplazado

   Por ejemplo, no se pueden reemplazar los anuncios integrados con anuncios de destino.
