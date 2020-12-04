---
seo-title: Resolución de problemas
title: Resolución de problemas
uuid: db76d6a4-c285-4d86-95a1-4f1a85ed3743
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Solución de problemas {#troubleshooting}

A continuación se indican los problemas comunes y las soluciones para la implementación:

* Si aparece el siguiente error:

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Asegúrese de que la contraseña se cifra mediante la clase proporcionada `ScrambleUtil`.

* Si aparece el siguiente error:

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Asegúrese de especificar la contraseña cifrada correcta para el archivo PFX.

* Si aparece el siguiente error:

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Asegúrese de que ha utilizado la clase de codificador de contraseña proporcionada con la implementación de referencia (esta utilidad de codificador es diferente de la que se proporciona con el servidor Adobe® Access™ para flujo protegido).

