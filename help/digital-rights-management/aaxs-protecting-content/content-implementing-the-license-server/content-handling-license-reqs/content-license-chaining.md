---
title: encadenamiento de licencias
description: encadenamiento de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# encadenado de licencias{#license-chaining}

Si la directiva utilizada para generar la licencia admite encadenamiento de licencias, el servidor debe decidir si emitir una licencia Leaf, una licencia Root o ambas. Para determinar qué tipo de encadenamiento de licencias admite una directiva, utilice `Policy.getLicenseChainType()` o llame a `Policy.getRootLicenseId()` para determinar si la directiva tiene una licencia raíz. Con la encadenación de licencias de Adobe Access 2.0, el servidor suele emitir una licencia de hoja la primera vez que el usuario solicita una licencia para un equipo en particular y una licencia raíz posteriormente. Para determinar si el equipo ya tiene una licencia de hoja para la directiva especificada, llame a `LicenseRequestMessage.clientHasLeafForPolicy()`.
