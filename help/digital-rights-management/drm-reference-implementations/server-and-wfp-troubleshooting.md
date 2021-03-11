---
title: Resolución de problemas
description: Resolución de problemas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Solución de problemas{#troubleshooting}

A continuación se indican algunos problemas y soluciones que puede encontrar durante la implementación.

* Si se muestra el siguiente mensaje de error:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Asegúrese de que la contraseña se haya cifrado con la clase `ScrambleUtil`.

* Si se muestra el siguiente mensaje de error:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Asegúrese de haber especificado la contraseña cifrada correcta en el archivo PFX.

* Si se muestra el siguiente mensaje de error:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Asegúrese de utilizar la clase *de codificador de contraseña que se ha proporcionado con la Implementación de referencia*. Esta utilidad de agitador es diferente de la que se proporciona con el servidor Adobe Primetime DRM para transmisión protegida.

