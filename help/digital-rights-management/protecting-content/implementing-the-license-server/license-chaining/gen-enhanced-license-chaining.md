---
title: Encadenado de licencias mejorado
description: Encadenado de licencias mejorado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Encadenado de licencias mejorado {#enhanced-license-chaining}

Si se utiliza una directiva DRM para generar una licencia compatible con la encadenación de licencias, el servidor debe decidir si emitir una licencia Leaf, una licencia Root o ambas. Si desea determinar qué tipo de encadenamiento de licencias admite una directiva DRM, debe utilizar `Policy.getLicenseChainType()` o llamar a `Policy.getRootLicenseId()` para determinar si la directiva DRM tiene una licencia raíz. Con la encadenación de licencias de Adobe Primetime DRM 2.0, el servidor suele emitir una licencia de hoja la primera vez que un usuario solicita una licencia para un equipo en particular y una licencia raíz posteriormente. Si desea determinar si el equipo ya tiene una licencia de hoja para la directiva especificada, debe llamar a `LicenseRequestMessage.clientHasLeafForPolicy()`.

Con la encadenación de licencias mejorada en Adobe Primetime DRM 3.0, se recomienda emitir una hoja y una raíz la primera vez que el usuario solicite una licencia para un equipo en particular. Si el usuario ya tiene la licencia Root, el servidor puede emitir solamente una hoja (llame a `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar si el cliente ya tiene una raíz mejorada 3.0). Para solicitudes de licencia posteriores, el cliente indica que ya tiene una hoja y una raíz, por lo que el servidor debe emitir una nueva licencia de raíz. Cuando se utiliza la cadena de licencia mejorada, se debe llamar a `setRootKeyRetrievalInfo()` para proporcionar las credenciales necesarias para descifrar la clave de cifrado raíz en la directiva DRM.

>[!NOTE]
>
>Si la directiva es compatible con el encadenado de licencias 3.0 mejorado, pero el cliente es Primetime DRM 2.0, el servidor emite una licencia encadenada original 2.0. Para determinar la versión del cliente, utilice `LicenseRequestMessage.getClientVersion()`.

