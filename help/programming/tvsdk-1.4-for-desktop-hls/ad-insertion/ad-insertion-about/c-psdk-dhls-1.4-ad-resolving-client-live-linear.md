---
description: Para el contenido en directo o lineal, TVSDK sustituye una parte del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.
seo-description: Para el contenido en directo o lineal, TVSDK sustituye una parte del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.
seo-title: Resolución e inserción de anuncios en directo/lineal
title: Resolución e inserción de anuncios en directo/lineal
uuid: 69f287aa-b707-442b-8e07-16f81b242c4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Resolución e inserción de anuncios en directo/lineal{#live-linear-ad-resolving-and-insertion}

Para el contenido en directo o lineal, TVSDK sustituye una parte del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.

Antes y durante la reproducción, TVSDK resuelve los anuncios conocidos, reemplaza partes del contenido principal con pausas publicitarias de la misma duración y, si es necesario, vuelve a calcular la línea de tiempo virtual. Las posiciones de los saltos de publicidad se especifican mediante puntos de referencia definidos por el manifiesto.

TVSDK inserta publicidades de las siguientes formas:

* **Anteponer**, que se encuentra al principio del contenido.
* **Mid-roll**, que se encuentra en medio del contenido.

TVSDK acepta la pausa publicitaria aunque la duración sea más larga o más corta que la duración de sustitución de puntos de referencia. De forma predeterminada, TVSDK admite el `#EXT-X-CUE` cue como un marcador de publicidad válido al resolver y colocar anuncios. Este marcador requiere el campo de metadatos `DURATION` en segundos y el identificador único de la señal. Por ejemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>Al implementar una norma habitual `AdPolicySelector`, se puede dar una política diferente a `AdBreakTimelineItem`las listas previas, intermedias y posteriores en `AdPolicyInfo`, que se basa en el tipo de `AdBreakTimelineItem`las listas. Por ejemplo, puede mantener el contenido de lanzamiento intermedio después de reproducirse, pero eliminar el contenido previo después de reproducirse.

Una vez iniciada la reproducción, el motor de vídeo actualiza periódicamente el archivo de manifiesto. TVSDK resuelve cualquier publicidad nueva e inserta la publicidad cuando se encuentra un punto de referencia en el flujo activo o lineal definido en el manifiesto. Después de resolver e insertar las publicidades, TVSDK vuelve a calcular la línea de tiempo virtual y distribuye un `TimelineEvent.TIMELINE_UPDATED` evento.
