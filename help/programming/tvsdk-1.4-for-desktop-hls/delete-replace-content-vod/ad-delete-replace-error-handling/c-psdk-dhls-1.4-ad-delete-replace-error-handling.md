---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-title: Gestión de errores de reemplazo y eliminación de publicidad
title: Gestión de errores de reemplazo y eliminación de publicidad
uuid: ab153591-0011-44b4-87f9-be0302c2295e
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Gestión de errores de reemplazo y eliminación de publicidad {#ad-deletion-and-replacement-error-handling}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.

TVSDK se ocupa de `timeRanges` los errores mediante la combinación y reordenación predeterminadas. En primer lugar, ordena los intervalos de tiempo definidos por el cliente según la *hora de inicio* . En función de este orden de clasificación, combina intervalos adyacentes y los une si hay subconjuntos e intersecciones entre los intervalos.

TVSDK gestiona los errores de intervalo de tiempo de la siguiente manera:

* Desordenado: TVSDK reordena los intervalos de tiempo.
* Subconjunto: TVSDK combina los subconjuntos de intervalo de tiempo.
* Intersección: TVSDK combina los intervalos de tiempo interrelacionados.
* Conflicto de intervalos de reemplazo: TVSDK elige la duración de reemplazo desde el primer lugar que aparece `timeRange` en el grupo en conflicto.

TVSDK gestiona los conflictos de modo de señalización de la siguiente manera:

* Si se definen intervalos REPLACE, TVSDK cambia automáticamente el modo de señalización a CUSTOM_RANGE.
* Si se definen intervalos DELETE o MARK y el modo de señalización es CUSTOM_RANGE, TVSDK elimina o marca estos rangos. En este caso no hay inserción de publicidad.
* Si un intervalo DELETE o MARK define una duración de sustitución, TVSDK ignora esta duración.

Cuando el servidor no devuelve un valor válido `AdBreaks`:

* TVSDK genera y procesa un `NOPTimelineOperation` para el vacío `AdBreak`. No se reproduce ningún anuncio.

## Ejemplos de errores de intervalo de tiempo {#time-range-error-examples}

TVSDK responde a especificaciones erróneas del intervalo de tiempo combinando o reemplazando los intervalos de tiempo según corresponda.

En el ejemplo siguiente, se definen cuatro intervalos de tiempo de ELIMINACIÓN que se intersectan. TVSDK combina los cuatro intervalos de tiempo en uno, de modo que el intervalo de eliminación real es de 0 a 50.

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

En el ejemplo siguiente, se definen cuatro intervalos de tiempo REPLACE con intervalos de tiempo que entran en conflicto. En este caso, TVSDK sustituye 0-50 por 25 anuncios. Va con la primera duración de reemplazo en el orden de clasificación, porque hay conflictos en intervalos posteriores.

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
