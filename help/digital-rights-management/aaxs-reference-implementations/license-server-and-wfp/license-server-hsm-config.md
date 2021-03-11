---
title: Configuración de HSM
description: Configuración de HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Configuración de HSM {#hsm-configuration}

No es obligatorio el uso de un HSM, pero se recomienda. La implementación de referencia se puede configurar para utilizar el proveedor Sun PKCS11 para la compatibilidad con HSM. Para utilizar una credencial en un HSM, debe crear un archivo de configuración para el proveedor Sun PKCS11. Consulte la documentación de Sun para obtener más información. Para comprobar que el archivo de configuración HSM y Sun PKCS11 están correctamente configurados, puede utilizar el siguiente comando (keytool está instalado con el JDK de Java):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente.

>[!NOTE]
>
>Desde Java 1.7, Sun Java de 64 bits para Windows no admite las interfaces PKCS11 que requiere el DRM de acceso de Adobe para comunicarse con dispositivos HSM. Si planea utilizar un HSM, utilice una versión de Java de 32 bits o un JDK que admita las interfaces PKCS11 completas.

