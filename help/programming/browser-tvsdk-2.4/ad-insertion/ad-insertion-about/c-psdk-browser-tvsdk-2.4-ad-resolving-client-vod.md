---
description: Para el contenido de vídeo bajo demanda (VOD), TVSDK del explorador inserta saltos de publicidad uniendo los anuncios en el contenido principal para que aumente la duración de la cronología.
title: Resolución e inserción de anuncios de VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Resolución e inserción de anuncios de VOD{#vod-ad-resolving-and-insertion}

Para el contenido de vídeo bajo demanda (VOD), TVSDK del explorador inserta saltos de publicidad uniendo los anuncios en el contenido principal para que aumente la duración de la cronología.

Antes de la reproducción, el TVSDK del explorador resuelve los anuncios conocidos, inserta y rompe el contenido principal tal como se describe en una cronología devuelta por Adobe Primetime ad decisioning y vuelve a calcular la cronología virtual, si es necesario.

TVSDK del explorador inserta anuncios de las siguientes maneras:

* **Pre-roll**, que se encuentra antes del contenido.
* **Post-roll**, que va después del contenido.

Después de que comience la reproducción, no se pueden producir cambios adicionales en el contenido. Los anuncios no pueden:

* Insertado
* Eliminado

  Por ejemplo, no puede eliminar anuncios integrados del contenido para ofrecer una experiencia sin anuncios.
* Reemplazado

  Por ejemplo, no se pueden reemplazar los anuncios integrados con anuncios de destino.
