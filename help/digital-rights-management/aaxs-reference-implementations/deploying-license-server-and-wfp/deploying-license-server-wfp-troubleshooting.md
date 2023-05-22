---
title: Solución de problemas
description: Solución de problemas
copied-description: true
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
