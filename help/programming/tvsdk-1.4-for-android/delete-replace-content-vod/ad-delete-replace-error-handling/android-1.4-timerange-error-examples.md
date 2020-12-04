---
description: TVSDK responde a especificaciones erróneas del intervalo de tiempo combinando o reemplazando los intervalos de tiempo según corresponda.
seo-description: TVSDK responde a especificaciones erróneas del intervalo de tiempo combinando o reemplazando los intervalos de tiempo según corresponda.
seo-title: Ejemplos de errores de intervalo de tiempo
title: Ejemplos de errores de intervalo de tiempo
uuid: 327b38dc-6aa3-49a7-b5e7-c343b704c5c3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Ejemplos de errores de intervalo de tiempo{#time-range-error-examples}

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

