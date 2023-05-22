---
description: Para el contenido de vídeo bajo demanda (VOD), TVSDK inserta saltos de publicidad uniendo los anuncios en el contenido principal para que aumente la duración de la cronología.
title: Resolución e inserción de un anuncio de VOD
exl-id: 10ae101d-f07b-485a-aa59-361761b4b65d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Resolución e inserción de anuncios de VOD {#resolve-and-insert-vod-ad}

Para el contenido de vídeo bajo demanda (VOD), TVSDK inserta saltos de publicidad uniendo los anuncios en el contenido principal para que aumente la duración de la cronología.

Antes de la reproducción, TVSDK resuelve los anuncios conocidos, inserta saltos de anuncios en el contenido principal tal como se describe en una cronología que devuelve Adobe Primetime ad decisioning y vuelve a calcular la cronología virtual, si es necesario.

TVSDK inserta anuncios de las siguientes maneras:

* **Pre-roll**, que se coloca antes del contenido.
* **Mid-roll**, que se encuentra en medio del contenido.
* **Post-roll**, que se coloca después del contenido.

>[!TIP]
>
>Después de que comience la reproducción, no se pueden producir cambios adicionales en el contenido.

Los anuncios no pueden:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar anuncios integrados del contenido para ofrecer una experiencia sin anuncios.
* Reemplazado

   Por ejemplo, no se pueden reemplazar los anuncios integrados con anuncios de destino.
