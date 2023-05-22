---
title: Encadenamiento de licencias
description: Encadenamiento de licencias
copied-description: true
exl-id: 2f439e21-c748-45aa-a87c-36e70ee3722a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Encadenamiento de licencias{#license-chaining}

Si la directiva utilizada para generar la licencia admite el encadenamiento de licencias, el servidor debe decidir si emitir una licencia de hoja, una licencia raíz o ambas. Para determinar qué tipo de licencia admite el encadenamiento de una directiva, utilice `Policy.getLicenseChainType()`, o llame a `Policy.getRootLicenseId()` para determinar si la directiva tiene una licencia raíz. Con el encadenamiento de licencias de Adobe Access 2.0, el servidor suele emitir una licencia hoja la primera vez que el usuario solicita una licencia para un equipo en particular y una licencia raíz a partir de entonces. Para determinar si el equipo ya tiene una licencia hoja para la directiva especificada, llame a `LicenseRequestMessage.clientHasLeafForPolicy()`.
