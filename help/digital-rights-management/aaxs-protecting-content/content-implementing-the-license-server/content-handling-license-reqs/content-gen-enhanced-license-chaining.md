---
title: Encadenamiento de licencias mejorado
description: Encadenamiento de licencias mejorado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Encadenamiento de licencias mejorado {#enhanced-license-chaining}

Con el encadenamiento de licencias mejorado en Adobe Access 3.0, se recomienda emitir una hoja y una raíz la primera vez que el usuario solicite una licencia para un equipo en particular. Si el usuario ya tiene la licencia Root, el servidor puede emitir solo una llamada Leaf (de ) `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar si el cliente ya tiene una raíz mejorada 3.0). Para las solicitudes de licencia posteriores, el cliente indicará que ya tiene una hoja y una raíz, por lo que el servidor debe emitir una nueva licencia de raíz. Cuando se utiliza el encadenamiento de licencias mejorado, `setRootKeyRetrievalInfo()` se debe llamar para proporcionar las credenciales necesarias para descifrar la clave de cifrado raíz en la directiva.

>[!NOTE]
>
>Si la directiva admite el encadenamiento de licencias mejorado 3.0, pero el cliente es Acceso de Adobe 2.0, el servidor emitirá una licencia encadenada original 2.0. Para determinar la versión del cliente, utilice LicenseRequestMessage.getClientVersion().
