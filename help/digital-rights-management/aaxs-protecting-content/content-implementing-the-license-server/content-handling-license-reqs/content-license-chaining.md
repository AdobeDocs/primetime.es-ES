---
title: Encadenamiento de licencias
description: Encadenamiento de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Encadenamiento de licencias{#license-chaining}

Si la directiva utilizada para generar la licencia admite el encadenamiento de licencias, el servidor debe decidir si emitir una licencia de hoja, una licencia de raíz o ambas. Para determinar qué tipo de licencia admite el encadenamiento de una directiva, utilice `Policy.getLicenseChainType()`, o llame a `Policy.getRootLicenseId()` para determinar si la directiva tiene una licencia raíz. Con el encadenamiento de licencias de Adobe Access 2.0, el servidor suele emitir una licencia hoja la primera vez que el usuario solicita una licencia para un equipo en particular y una licencia raíz a partir de entonces. Para determinar si el equipo ya tiene una licencia hoja para la directiva especificada, llame a `LicenseRequestMessage.clientHasLeafForPolicy()`.
