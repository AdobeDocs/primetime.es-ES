---
title: Encadenamiento de licencias mejorado
description: Encadenamiento de licencias mejorado
copied-description: true
exl-id: 4b07b29c-e739-4bf9-b464-0c82f68542d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Encadenamiento de licencias mejorado {#enhanced-license-chaining}

Si se utiliza una directiva DRM para generar una licencia que admita el encadenamiento de licencias, el servidor debe decidir si emite una licencia de hoja, una licencia raíz o ambas. Si desea determinar qué tipo de licencia admite el encadenamiento de una directiva DRM, debe utilizar `Policy.getLicenseChainType()`, o llame a `Policy.getRootLicenseId()` para determinar si la directiva DRM tiene una licencia raíz. Con la encadenación de licencias de Adobe Primetime DRM 2.0, el servidor suele emitir una licencia hoja la primera vez que un usuario solicita una licencia para un equipo en particular y una licencia raíz a partir de entonces. Si desea determinar si el equipo ya tiene una licencia hoja para la directiva especificada, debe llamar a `LicenseRequestMessage.clientHasLeafForPolicy()`.

Con el encadenamiento de licencias mejorado en Adobe Primetime DRM 3.0, se recomienda emitir una hoja y una raíz la primera vez que el usuario solicite una licencia para una máquina en particular. Si el usuario ya tiene la licencia Root, el servidor puede emitir solo una llamada Leaf (de ) `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar si el cliente ya tiene una raíz mejorada 3.0). Para las solicitudes de licencia posteriores, el cliente indica que ya tiene una hoja y una raíz, por lo que el servidor debe emitir una nueva licencia de raíz. Cuando se utiliza el encadenamiento de licencias mejorado, `setRootKeyRetrievalInfo()` Se debe llamar a para proporcionar las credenciales necesarias para descifrar la clave de cifrado raíz en la directiva DRM.

>[!NOTE]
>
>Si la directiva admite el encadenamiento de licencias mejorado 3.0, pero el cliente es Primetime DRM 2.0, el servidor emite una licencia encadenada original 2.0. Para determinar la versión del cliente, utilice `LicenseRequestMessage.getClientVersion()`.
