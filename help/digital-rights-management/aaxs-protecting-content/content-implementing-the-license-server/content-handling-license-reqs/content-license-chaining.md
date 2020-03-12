---
seo-title: encadenamiento de licencias
title: encadenamiento de licencias
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# encadenamiento de licencias{#license-chaining}

Si la política utilizada para generar la licencia admite encadenamiento de licencias, el servidor debe decidir si emitir una licencia Leaf, una licencia Root o ambas. Para determinar qué tipo de encadenamiento de licencias admite, utilice `Policy.getLicenseChainType()`o llame `Policy.getRootLicenseId()` para determinar si la directiva tiene una licencia raíz. Con la cadena de licencias de Adobe Access 2.0, el servidor suele emitir una licencia de hoja la primera vez que el usuario solicita una licencia para un equipo en particular y una licencia raíz posteriormente. Para determinar si la máquina ya tiene una licencia de hoja para la directiva especificada, llame a `LicenseRequestMessage.clientHasLeafForPolicy()`.
