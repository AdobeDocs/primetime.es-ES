---
description: Para el contenido de vídeo a petición (VOD), el SDK de TVSDK del explorador inserta y divide las publicidades del contenido principal para que la duración de la línea de tiempo aumente.
seo-description: Para el contenido de vídeo a petición (VOD), el SDK de TVSDK del explorador inserta y divide las publicidades del contenido principal para que la duración de la línea de tiempo aumente.
seo-title: Resolución e inserción de anuncios de VOD
title: Resolución e inserción de anuncios de VOD
uuid: 34a30ae5-d553-4c5d-9829-8e5eaa41c104
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Resolución e inserción de anuncios de VOD{#vod-ad-resolving-and-insertion}

Para el contenido de vídeo a petición (VOD), el SDK de TVSDK del explorador inserta y divide las publicidades del contenido principal para que la duración de la línea de tiempo aumente.

Antes de la reproducción, el SDK de TVSDK del explorador resuelve anuncios conocidos, inserta y rompe el contenido principal tal como se describe en una línea de tiempo que se devuelve de Adobe Primetime y toma decisiones, y vuelve a calcular la línea de tiempo virtual, si es necesario.

El SDK de TVSDK de explorador inserta publicidades de las siguientes formas:

* **Anteponer**, que está antes del contenido.
* **Post-roll**, que se encuentra después del contenido.

Una vez iniciada la reproducción, no se pueden producir cambios adicionales en el contenido. Las publicidades no pueden ser:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar las publicidades integradas del contenido para ofrecer una experiencia sin publicidad.
* Reemplazado

   Por ejemplo, no puede reemplazar las publicidades integradas con las publicidades de objetivo.

