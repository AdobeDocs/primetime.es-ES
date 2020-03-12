---
description: Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.
seo-description: Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.
seo-title: Resolución e inserción de anuncios de VOD
title: Resolución e inserción de anuncios de VOD
uuid: c1017483-5b4f-4d71-9589-fb2327b4572b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Resolución e inserción de anuncios de VOD{#vod-ad-resolving-and-insertion}

Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.

Antes de la reproducción, TVSDK resuelve anuncios conocidos, inserta y rompe el contenido principal como se describe en una línea de tiempo devuelta por TVSDK y, si es necesario, vuelve a calcular la línea de tiempo virtual.

TVSDK inserta publicidades de las siguientes formas:

* **Anteponer**, que está antes del contenido.
* **Mid-roll**, que está en el contenido.
* **Post-roll**, que se encuentra después del contenido.

>[!IMPORTANT]
>
>Al implementar una personalización `AdPolicySelector`, se puede dar una directiva diferente a cada tipo de `AdBreakTimelineItem` (previo, intermedio o posterior) en `AdPolicyInfo`, según el tipo de `AdBreakTimelineItem`. Por ejemplo, puede mantener el contenido de lanzamiento intermedio después de reproducirse pero eliminar el contenido previo después de reproducirse.

Una vez iniciada la reproducción, no se pueden producir cambios adicionales en el contenido. Las publicidades no pueden ser:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar las publicidades integradas del contenido para ofrecer una experiencia sin publicidad.
* Reemplazado

   Por ejemplo, no puede reemplazar las publicidades integradas con las publicidades de objetivo.

