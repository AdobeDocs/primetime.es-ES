---
description: TVSDK responde a especificaciones erróneas del intervalo de tiempo combinando o reemplazando los intervalos de tiempo según corresponda.
seo-description: TVSDK responde a especificaciones erróneas del intervalo de tiempo combinando o reemplazando los intervalos de tiempo según corresponda.
seo-title: Ejemplos de errores de intervalo de tiempo
title: Ejemplos de errores de intervalo de tiempo
uuid: f6cc1e61-8f42-4559-b643-2134180a8c5e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Ejemplos de errores de intervalo de tiempo{#time-range-error-examples}

TVSDK responde a especificaciones erróneas del intervalo de tiempo combinando o reemplazando los intervalos de tiempo según corresponda.

**ELIMINAR intervalo de tiempo**

En el ejemplo siguiente, se definen cuatro intervalos de tiempo de ELIMINACIÓN que se intersectan. TVSDK combina los cuatro intervalos de tiempo en uno, de modo que el intervalo de eliminación real es de 0 a 50.

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

En el ejemplo siguiente, se definen cuatro intervalos de tiempo REPLACE con intervalos de tiempo que entran en conflicto. En este caso, TVSDK sustituye 0-50 por 25 anuncios. Va con la primera duración de reemplazo en el orden de clasificación, porque hay conflictos en intervalos posteriores.

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

