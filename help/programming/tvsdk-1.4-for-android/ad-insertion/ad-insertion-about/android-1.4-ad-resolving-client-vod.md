---
description: Para el contenido de vídeo bajo demanda (VOD), TVSDK inserta los saltos de publicidad duplicando los anuncios en el contenido principal, de modo que la duración de la cronología aumente.
title: Resolución e inserción de anuncios de VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Resolución e inserción de anuncios de VOD{#vod-ad-resolving-and-insertion}

Para el contenido de vídeo bajo demanda (VOD), TVSDK inserta los saltos de publicidad duplicando los anuncios en el contenido principal, de modo que la duración de la cronología aumente.

Antes de la reproducción, TVSDK resuelve anuncios conocidos, inserta y rompe el contenido principal tal como se describe en una cronología devuelta por Adobe Primetime al tomar decisiones de anuncios y, si es necesario, vuelve a calcular la cronología virtual.

TVSDK inserta anuncios de las siguientes maneras:

* **Anuncio previo a la emisión**, que se encuentra antes del contenido.
* **Mid-roll**, que está en el contenido.
* **Anuncio**, que se encuentra después del contenido.

Una vez iniciada la reproducción, no se pueden producir cambios adicionales en el contenido. Los anuncios no pueden ser:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar anuncios integrados del contenido para ofrecer una experiencia sin publicidad.
* Reemplazado

   Por ejemplo, no se pueden reemplazar los anuncios integrados por anuncios orientados.

