---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.
seo-title: Gestión de errores de reemplazo y eliminación de publicidad
title: Gestión de errores de reemplazo y eliminación de publicidad
uuid: e2e06f13-9813-4d86-b6fe-3d09f3bdb100
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Administración de errores de reemplazo y eliminación de publicidad{#ad-deletion-and-replacement-error-handling}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.

TVSDK trata los errores `timeRanges` mediante la combinación y reordenación predeterminadas. En primer lugar, ordena los intervalos de tiempo definidos por el cliente por la hora *de inicio*. En función de este orden de clasificación, combina intervalos adyacentes y los une si hay subconjuntos e intersecciones entre los intervalos.

TVSDK gestiona los errores de intervalo de tiempo de la siguiente manera:

* Desordenado: TVSDK reordena los intervalos de tiempo.
* Subconjunto: TVSDK combina los subconjuntos de intervalo de tiempo.
* Intersección: TVSDK combina los intervalos de tiempo interrelacionados.
* Conflicto de intervalos de reemplazo: TVSDK elige la duración de reemplazo desde la primera vez que aparece `timeRange` en el grupo en conflicto.

TVSDK gestiona los conflictos de modo de señalización con metadatos de anuncio de la siguiente manera:

* Si el modo de señalización de publicidad entra en conflicto con los metadatos del intervalo de tiempo, los metadatos del intervalo de tiempo siempre tienen prioridad. Por ejemplo: si el modo de señalización de publicidad está configurado como mapa del servidor o como señales de manifiesto, y también hay intervalos de tiempo MARK en los metadatos de publicidad, el comportamiento resultante es que los intervalos están marcados y no se insertan anuncios.
* Para los intervalos REPLACE, si el modo de señalización se establece como mapa del servidor o como señales de manifiesto, los intervalos se reemplazan como se especifica en los rangos REPLACE y no hay inserción de anuncios a través de mapas del servidor o señales de manifiesto. Consulte [Modo de señalización de publicidad](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

Cuando el servidor no devuelve un valor válido `AdBreaks`:

* TVSDK genera y procesa un `NOPTimelineOperation` para el `AdBreak` vacío. No se reproduce ningún anuncio.

Para intervalos de tiempo con flujos en directo:

* Aunque esta función de eliminación/reemplazo de anuncios en C3 está pensada para que solo sea compatible con VOD, los intervalos de tiempo se procesan para flujos en directo, así como si se especifican en los metadatos de anuncio.

## Ejemplos de error de intervalo de tiempo {#time-range-error-examples}

TVSDK responde a especificaciones erróneas del intervalo de tiempo combinando o reemplazando los intervalos de tiempo según corresponda.

En el ejemplo siguiente, se definen cuatro intervalos de tiempo de DELETE que se intersectan. TVSDK combina los cuatro intervalos de tiempo en uno, de modo que el intervalo de eliminación real es de 0 a 50.

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
