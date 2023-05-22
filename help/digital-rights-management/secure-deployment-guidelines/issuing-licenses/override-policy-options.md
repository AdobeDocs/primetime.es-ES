---
description: Al emitir una licencia, el servidor de licencias puede anular las reglas de uso especificadas en la directiva.
title: Anular opciones de directiva
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Anular opciones de directiva{#overriding-policy-options}

Al emitir una licencia, el servidor de licencias puede anular las reglas de uso especificadas en la directiva.

Si la directiva especifica una fecha de inicio, no se genera una licencia antes de esa fecha de inicio. Sin embargo, puede establecer una fecha de inicio futura en la licencia una vez generada la licencia. Esta opción debe utilizarse con precaución porque el cliente no puede impedir que el usuario avance el tiempo del sistema para evitar la fecha de inicio.
