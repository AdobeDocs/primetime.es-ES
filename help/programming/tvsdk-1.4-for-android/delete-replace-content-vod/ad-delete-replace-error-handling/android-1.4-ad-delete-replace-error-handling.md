---
description: TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.
title: Gestión de errores de reemplazo y eliminación de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Gestión de errores de eliminación y reemplazo de publicidad{#ad-deletion-and-replacement-error-handling}

TVSDK gestiona los errores de intervalo de tiempo según el problema específico, combinando o reordenando los intervalos de tiempo incorrectamente definidos.

TVSDK trata los errores `timeRanges` al realizar la combinación y reordenación predeterminadas. En primer lugar, ordena los intervalos de tiempo definidos por el cliente por la *hora de inicio*. En función de este orden de clasificación, combina intervalos adyacentes y los une si hay subconjuntos e intersecciones entre los intervalos.

TVSDK gestiona los errores de intervalo de tiempo de la siguiente manera:

* Fuera de orden: TVSDK reordena los intervalos de tiempo.
* Subconjunto: TVSDK combina los subconjuntos de intervalo de tiempo.
* Intersección : TVSDK combina los intervalos de tiempo que se intersectan.
* Conflicto de intervalos de reemplazo : TVSDK elige la duración de reemplazo desde la primera vez que aparece `timeRange` en el grupo en conflicto.

TVSDK gestiona los conflictos del modo de señalización con los metadatos de publicidad de la siguiente manera:

* Si el modo de señalización de anuncio entra en conflicto con los metadatos del intervalo de tiempo, estos siempre tienen prioridad. Por ejemplo, si el modo de señalización de publicidad está establecido como mapa del servidor o señal de manifiesto y también hay intervalos de tiempo MARK en los metadatos de publicidad, el comportamiento resultante es que los intervalos están marcados y no se insertan anuncios.
* En los intervalos REPLACE, si el modo de señalización está definido como mapa del servidor o como señales de manifiesto, los intervalos se sustituyen según se especifica en los intervalos REPLACE y no hay inserción de anuncios a través del mapa del servidor o las indicaciones de manifiesto. Consulte [Modo de señalización de publicidad](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

Cuando el servidor no devuelve un `AdBreaks` válido:

* TVSDK genera y procesa un `NOPTimelineOperation` para el `AdBreak` vacío. No se reproduce ningún anuncio.

Para intervalos de tiempo con flujos en directo:

* Aunque esta función de eliminación/reemplazo de anuncios C3 está pensada para ser compatible únicamente con VOD, los intervalos de tiempo se procesan también para transmisiones en directo si se especifican en los metadatos de los anuncios.

## Ejemplos de error de intervalo de tiempo {#time-range-error-examples}

TVSDK responde a especificaciones de intervalo de tiempo erróneas combinando o reemplazando los intervalos de tiempo según corresponda.

En el ejemplo siguiente, se definen cuatro intervalos de tiempo de DELETE que se intersectan. TVSDK combina los cuatro intervalos de tiempo en uno, de modo que el intervalo de eliminación real es de 0 a 50 segundos.

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

En el siguiente ejemplo, cuatro intervalos de tiempo REPLACE se definen con intervalos de tiempo conflictivos. En este caso, TVSDK reemplaza 0-50s por 25s de anuncios. Va con la primera duración de reemplazo en el orden de clasificación, ya que hay conflictos en intervalos posteriores.

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
