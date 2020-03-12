---
description: 'null'
seo-description: 'null'
seo-title: Resolución de problemas
title: Resolución de problemas
uuid: 06b86067-1ff6-4b4e-922f-7f968260ba19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Resolución de problemas{#troubleshooting}

A continuación se indican algunos problemas y soluciones que puede encontrar durante la implementación.

* Si se muestra el siguiente mensaje de error:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Asegúrese de que la contraseña se ha cifrado con la `ScrambleUtil` clase.

* Si se muestra el siguiente mensaje de error:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Asegúrese de que ha especificado la contraseña cifrada correcta en el archivo PFX.

* Si se muestra el siguiente mensaje de error:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Asegúrese de utilizar la clase de codificador de contraseñas *que se ha proporcionado con la implementación* de referencia. Esta utilidad de reproductor de secuencias de comandos es diferente de la que se proporciona con el servidor DRM de Adobe Primetime para flujo protegido.

