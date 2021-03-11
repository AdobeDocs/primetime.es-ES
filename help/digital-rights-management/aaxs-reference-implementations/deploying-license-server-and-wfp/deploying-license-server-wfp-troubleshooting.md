---
title: Resolución de problemas
description: Resolución de problemas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Solución de problemas {#troubleshooting}

A continuación se enumeran los problemas comunes y las soluciones para la implementación:

* Si ve el siguiente error:

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Asegúrese de que la contraseña esté cifrada utilizando la clase proporcionada `ScrambleUtil`.

* Si ve el siguiente error:

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Asegúrese de especificar la contraseña cifrada correcta para el archivo PFX.

* Si ve el siguiente error:

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Asegúrese de que ha utilizado la clase de codificador de contraseña que se proporciona con la Implementación de referencia (esta utilidad de desguace es diferente de la que se proporciona con el servidor Adobe® Access™ para transmisión protegida).

