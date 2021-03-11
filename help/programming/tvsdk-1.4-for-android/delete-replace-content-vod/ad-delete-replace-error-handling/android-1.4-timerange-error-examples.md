---
description: TVSDK responde a especificaciones de intervalo de tiempo erróneas combinando o reemplazando los intervalos de tiempo según corresponda.
title: Ejemplos de error de intervalo de tiempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Ejemplos de error de intervalo de tiempo{#time-range-error-examples}

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

