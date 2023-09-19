---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico, ya sea combinando o reordenando los intervalos de tiempo definidos incorrectamente.
title: Gestión de errores de eliminación y sustitución de anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Gestión de errores de eliminación y sustitución de anuncios{#ad-deletion-and-replacement-error-handling}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico, ya sea combinando o reordenando los intervalos de tiempo definidos incorrectamente.

TVSDK trata con `timeRanges` errores al realizar la combinación y reordenación predeterminadas. En primer lugar, ordena los intervalos de tiempo definidos por el cliente por la variable *comenzar* hora. En función de este orden de clasificación, combina intervalos adyacentes y los une si hay subconjuntos e intersecciones entre los intervalos.

TVSDK gestiona los errores de intervalo de tiempo de la siguiente manera:

* Desordenado: TVSDK reordena los intervalos de tiempo.
* Subconjunto: TVSDK combina los subconjuntos de intervalo de tiempo.
* Intersect: TVSDK combina los intervalos de tiempo de intersección.
* Conflicto de reemplazo de intervalos: TVSDK elige la duración de reemplazo de la primera que aparece `timeRange` en el grupo en conflicto.

TVSDK gestiona los conflictos del modo de señalización con los metadatos de publicidad de la siguiente manera:

* Si el modo de señalización de publicidad entra en conflicto con los metadatos de intervalo de tiempo, estos siempre tienen prioridad. Por ejemplo, si el modo de señalización de publicidad se establece como mapa del servidor o señales de manifiesto y también hay intervalos de tiempo MARK en los metadatos de publicidad, el comportamiento resultante es que los intervalos se marcan y no se insertan anuncios.
* En el caso de los intervalos REPLACE, si el modo de señalización está establecido como mapa del servidor o señales de manifiesto, los intervalos se reemplazan según se especifica en los intervalos REPLACE y no hay inserción de anuncios a través de las señales de mapa del servidor o de manifiesto. Consulte [Modo de señalización de anuncio](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

Cuando el servidor no devuelve datos válidos `AdBreaks`:

* TVSDK genera y procesa un `NOPTimelineOperation` para el vacío `AdBreak`. No se reproduce ningún anuncio.

Para intervalos de tiempo con emisiones en directo:

* Aunque esta función de eliminación/sustitución de anuncios de C3 está pensada para ser compatible únicamente con VOD, los intervalos de tiempo se procesan para emisiones en directo, así si se especifican en los metadatos de la publicidad.

## Ejemplos de error de intervalo de tiempo {#time-range-error-examples}

TVSDK responde a especificaciones de intervalo de tiempo erróneas combinando o reemplazando los intervalos de tiempo según corresponda.

En el ejemplo siguiente, se definen cuatro intervalos de tiempo del DELETE que se intersectan. TVSDK combina los cuatro intervalos de tiempo en uno, de modo que el intervalo de eliminación real está entre 0 y 50 segundos.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000
    }, {
        "begin": 20000,
        "end": 50000
    }, {
        "begin": 0,
        "end": 30000
    }, {
        "begin": 30000,
        "end": 40000
    } ]
}
```

En el ejemplo siguiente, se definen cuatro intervalos de tiempo REEMPLAZAR con intervalos de tiempo en conflicto. En este caso, TVSDK reemplaza el 0-50 con 25 anuncios. Va con la primera duración de reemplazo en el criterio de ordenación, ya que hay conflictos en los intervalos posteriores.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000,
        "replace-duration": 15000
    }, {
        "begin": 20000,
        "end": 50000,
        "replace-duration": 20000
    }, {
        "begin": 0,
        "end": 30000,
        "replace-duration": 25000
    }, {
        "begin": 30000,
        "end": 40000,
        "replace-duration": 30000
    } ]
}
```
