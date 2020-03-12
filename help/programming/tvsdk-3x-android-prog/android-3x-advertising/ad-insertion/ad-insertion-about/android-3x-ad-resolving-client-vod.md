---
description: Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.
seo-description: Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.
seo-title: Resolver e insertar anuncios de VOD
title: Resolver e insertar anuncios de VOD
uuid: b7124cab-441b-4b38-ac83-300ab9e5f9ec
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Resolver e insertar anuncios de VOD {#resolve-and-insert-vod-ad}

Para el contenido de vídeo a petición (VOD), TVSDK inserta y divide las publicidades empalmándolas en el contenido principal para que la duración de la línea de tiempo aumente.

Antes de la reproducción, TVSDK resuelve anuncios conocidos, inserta y rompe el contenido principal como se describe en una línea de tiempo que se devuelve de Adobe Primetime y toma decisiones, y vuelve a calcular la línea de tiempo virtual, si es necesario.

TVSDK inserta publicidades de las siguientes formas:

* **Anteponer**, que se coloca antes del contenido.
* **Mid-roll**, que se encuentra en medio del contenido.
* **Post-roll**, que se coloca después del contenido.

>[!TIP]
>
>Una vez iniciada la reproducción, no se pueden producir cambios adicionales en el contenido.

Las publicidades no pueden ser:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar las publicidades integradas del contenido para ofrecer una experiencia sin publicidad.
* Reemplazado

   Por ejemplo, no puede reemplazar las publicidades integradas con las publicidades de objetivo.