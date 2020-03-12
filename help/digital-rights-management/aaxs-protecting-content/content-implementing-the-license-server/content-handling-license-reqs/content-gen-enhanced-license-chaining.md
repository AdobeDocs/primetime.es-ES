---
seo-title: Encadenamiento de licencias mejorado
title: Encadenamiento de licencias mejorado
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: da8736769f7b47318dbd955aa854f83ae64d6d7b

---


# Encadenamiento de licencias mejorado {#enhanced-license-chaining}

Con la encadenación de licencias mejorada en Adobe Access 3.0, se recomienda emitir una hoja y una raíz la primera vez que el usuario solicite una licencia para un equipo en particular. Si el usuario ya tiene la licencia de raíz, el servidor puede emitir sólo una hoja (llame `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar si el cliente ya tiene una raíz mejorada 3.0). Para solicitudes de licencia posteriores, el cliente indicará que ya tiene una hoja y una raíz, por lo que el servidor debe emitir una nueva licencia de raíz. Cuando se utiliza la cadena de licencia mejorada, se debe llamar `setRootKeyRetrievalInfo()` para proporcionar las credenciales necesarias para descifrar la clave de cifrado raíz en la directiva.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Si la directiva admite el encadenado de licencias mejorado 3.0, pero el cliente es Adobe Access 2.0, el servidor emitirá una licencia encadenada original 2.0. Para determinar la versión del cliente, utilice LicenseRequestMessage.getClientVersion().

