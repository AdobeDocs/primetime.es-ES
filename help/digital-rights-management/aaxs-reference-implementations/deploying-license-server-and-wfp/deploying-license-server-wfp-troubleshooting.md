---
title: Solución de problemas
description: Solución de problemas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Solución de problemas {#troubleshooting}

A continuación se enumeran problemas comunes y soluciones para la implementación:

* Si ve el siguiente error:

  ```
      "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  Asegúrese de que la contraseña esté cifrada con el proporcionado `ScrambleUtil` clase.

* Si ve el siguiente error:

  ```
      "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Asegúrese de especificar la contraseña cifrada correcta para el archivo PFX.

* Si ve el siguiente error:

  ```
      "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Asegúrese de utilizar la clase de codificador de contraseñas que se proporciona con la Implementación de referencia (esta utilidad de codificador es diferente de la que se proporciona con el servidor Adobe ® Access™ para flujo protegido).
