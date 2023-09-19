---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico, ya sea combinando o reordenando los intervalos de tiempo definidos incorrectamente.
title: Gestión de errores de eliminación y sustitución de anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Gestión de errores de eliminación y sustitución de anuncios {#ad-deletion-and-replacement-error-handling}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico, ya sea combinando o reordenando los intervalos de tiempo definidos incorrectamente.

TVSDK trata con `timeRanges` errores al realizar la combinación y reordenación predeterminadas. En primer lugar, ordena los intervalos de tiempo definidos por el cliente por la variable *comenzar* hora. En función de este orden de clasificación, combina intervalos adyacentes y los une si hay subconjuntos e intersecciones entre los intervalos.

TVSDK gestiona los errores de intervalo de tiempo de la siguiente manera:

* Desordenado: TVSDK reordena los intervalos de tiempo.
* Subconjunto: TVSDK combina los subconjuntos de intervalo de tiempo.
* Intersect: TVSDK combina los intervalos de tiempo de intersección.
* Conflicto de reemplazo de intervalos: TVSDK elige la duración de reemplazo de la primera que aparece `timeRange` en el grupo en conflicto.

TVSDK gestiona los conflictos del modo de señalización de la siguiente manera:

* Si se definen intervalos REPLACE, TVSDK cambia automáticamente el modo de señalización a CUSTOM_RANGE.
* Si se definen intervalos de DELETE o intervalos de MARK y el modo de señalización es CUSTOM_RANGE, TVSDK elimina o marca estos intervalos. En este caso, no hay inserción de publicidad.
* Si un rango de DELETE o un rango de MARK define una duración de reemplazo, TVSDK la ignorará.

Cuando el servidor no devuelve datos válidos `AdBreaks`:

* TVSDK genera y procesa un `NOPTimelineOperation` para el vacío `AdBreak`. No se reproduce ningún anuncio.

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
