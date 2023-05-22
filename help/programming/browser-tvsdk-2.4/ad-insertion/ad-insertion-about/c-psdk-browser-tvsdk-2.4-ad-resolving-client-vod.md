---
description: Para el contenido de vídeo bajo demanda (VOD), TVSDK del explorador inserta saltos de publicidad uniendo los anuncios en el contenido principal para que aumente la duración de la cronología.
title: Resolución e inserción de anuncios de VOD
exl-id: c2a2f14b-c90d-47fc-9dcc-eff8b1491dde
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

Después de que comience la reproducción, no se pueden producir cambios adicionales en el contenido. Los anuncios no pueden ser:

* Insertado
* Eliminado

   Por ejemplo, no puede eliminar anuncios integrados del contenido para ofrecer una experiencia sin anuncios.
* Reemplazado

   Por ejemplo, no se pueden reemplazar los anuncios integrados con anuncios de destino.
