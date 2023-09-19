---
description: TVSDK responde a especificaciones de intervalo de tiempo erróneas combinando o reemplazando los intervalos de tiempo según corresponda.
title: Ejemplos de error de intervalo de tiempo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Ejemplos de error de intervalo de tiempo{#time-range-error-examples}

TVSDK responde a especificaciones de intervalo de tiempo erróneas combinando o reemplazando los intervalos de tiempo según corresponda.

**Intervalo de tiempo del DELETE**

En el ejemplo siguiente, se definen cuatro intervalos de tiempo del DELETE que se intersectan. TVSDK combina los cuatro intervalos de tiempo en uno, de modo que el intervalo de eliminación real está entre 0 y 50 segundos.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}
```

**REEMPLAZAR intervalo de tiempo**

En el ejemplo siguiente, se definen cuatro intervalos de tiempo REEMPLAZAR con intervalos de tiempo en conflicto. En este caso, TVSDK reemplaza el 0-50 con 25 anuncios. Va con la primera duración de reemplazo en el criterio de ordenación, ya que hay conflictos en los intervalos posteriores.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}
```
