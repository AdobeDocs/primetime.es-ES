---
description: Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.
seo-description: Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.
seo-title: Resolución e inserción de anuncios de VOD
title: Resolución e inserción de anuncios de VOD
uuid: 33280792-ad08-41c1-b180-cc2159e8137c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Resolución e inserción de anuncios de VOD{#vod-ad-resolving-and-insertion}

Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.

Antes de la reproducción, TVSDK resuelve anuncios conocidos, inserta y rompe el contenido principal como se describe en una línea de tiempo que se devuelve de Adobe Primetime y toma decisiones, y vuelve a calcular la línea de tiempo virtual, si es necesario.

TVSDK inserta publicidades de las siguientes formas:

* **Anteponer**, que está antes del contenido.
* **Mid-roll**, que está en el contenido.
* **Post-roll**, que se encuentra después del contenido.

Una vez iniciada la reproducción, no se pueden producir cambios adicionales en el contenido. Las publicidades no pueden ser:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar las publicidades integradas del contenido para ofrecer una experiencia sin publicidad.
* Reemplazado

   Por ejemplo, no puede reemplazar las publicidades integradas con las publicidades de objetivo.

