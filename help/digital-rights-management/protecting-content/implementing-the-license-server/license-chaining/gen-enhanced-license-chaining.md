---
seo-title: Encadenamiento de licencias mejorado
title: Encadenamiento de licencias mejorado
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Encadenamiento de licencias mejorado {#enhanced-license-chaining}

Si se utiliza una directiva DRM para generar una licencia compatible con la encadenación de licencias, el servidor debe decidir si emitir una licencia Leaf, una licencia Root o ambas. Si desea determinar qué tipo de encadenado de licencias admite una directiva DRM, debe utilizar `Policy.getLicenseChainType()`o llamar `Policy.getRootLicenseId()` para determinar si la directiva DRM tiene una licencia raíz. Con la cadena de licencias DRM 2.0 de Adobe Primetime, el servidor suele emitir una licencia de hoja la primera vez que un usuario solicita una licencia para un equipo en particular y una licencia raíz posteriormente. Si desea determinar si la máquina ya tiene una licencia de hoja para la directiva especificada, debe llamar a `LicenseRequestMessage.clientHasLeafForPolicy()`.

Con la encadenación de licencias mejorada en Adobe Primetime DRM 3.0, se recomienda emitir una hoja y una raíz la primera vez que el usuario solicite una licencia para un equipo en particular. Si el usuario ya tiene la licencia de raíz, el servidor puede emitir sólo una hoja (llame `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar si el cliente ya tiene una raíz mejorada 3.0). Para solicitudes de licencia posteriores, el cliente indica que ya tiene una hoja y una raíz, por lo que el servidor debe emitir una nueva licencia de raíz. Cuando se utiliza la cadena de licencia mejorada, se debe llamar `setRootKeyRetrievalInfo()` para proporcionar las credenciales necesarias para descifrar la clave de cifrado raíz en la directiva DRM.

>[!NOTE]
>
>Si la directiva admite el encadenado de licencias mejorado 3.0, pero el cliente es Primetime DRM 2.0, el servidor emite una licencia encadenada original 2.0. Para determinar la versión del cliente, utilice `LicenseRequestMessage.getClientVersion()`.

