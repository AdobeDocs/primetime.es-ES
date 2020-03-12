---
description: Puede anular el comportamiento predeterminado de la forma en que TVSDK busca por encima de las publicidades al utilizar marcadores de publicidad personalizados.
seo-description: Puede anular el comportamiento predeterminado de la forma en que TVSDK busca por encima de las publicidades al utilizar marcadores de publicidad personalizados.
seo-title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
title: Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados
uuid: 926299c6-9c23-457d-b836-08432e4e169e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Controlar el comportamiento de reproducción para buscar por encima de los marcadores de publicidad personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puede anular el comportamiento predeterminado de la forma en que TVSDK busca por encima de las publicidades al utilizar marcadores de publicidad personalizados.

De forma predeterminada, cuando un usuario busca en secciones de publicidad anteriores o en secciones de publicidad que resultan de la colocación de marcadores de publicidad personalizados, TVSDK omite las publicidades. Esto puede diferir del comportamiento de reproducción actual de los saltos de publicidad estándar.

Puede indicar a TVSDK que cambie la posición del cursor de reproducción al principio de la última publicidad personalizada omitida cuando el usuario busque más anuncios personalizados.

1. Configure una instancia de metadatos con la `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumeración establecida en el valor de cadena &quot;true&quot; (no como booleano `true`).

1. Cree y configure una `MediaResource` instancia, pasando las opciones de configuración adicionales a `TimeRangeCollection.toMetadata`. Este método recibe opciones de configuración adicionales mediante otra estructura de metadatos genérica.

