---
title: Solución de problemas
description: Solución de problemas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

  Asegúrese de que la contraseña se haya cifrado con `ScrambleUtil` clase.

* Si se muestra el siguiente mensaje de error:

  ```
  "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Asegúrese de haber especificado la contraseña cifrada correcta en el archivo PFX.

* Si se muestra el siguiente mensaje de error:

  ```
  "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Asegúrese de utilizar la clase codificador de contraseñas *que se ha proporcionado con la Implementación de referencia*. Esta utilidad de codificador es diferente de la que se ha proporcionado con el servidor DRM de Adobe Primetime para flujo protegido.
