---
title: Configuración de HSM
description: Configuración de HSM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Configuración de HSM {#hsm-configuration}

No se requiere el uso de un HSM, pero se recomienda. La implementación de referencia se puede configurar para que utilice el proveedor Sun PKCS11 para la compatibilidad con HSM. Para utilizar una credencial en un HSM, debe crear un archivo de configuración para el proveedor Sun PKCS11. Consulte la documentación de Sun para obtener más información. Para comprobar que el archivo de configuración de HSM y Sun PKCS11 está configurado correctamente, puede utilizar el siguiente comando (keytool se instala con el JDK de Java):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM estará configurado correctamente.

>[!NOTE]
>
>A partir de Java 1.7, Sun Java de 64 bits para Windows no admite las interfaces PKCS11 que requiere DRM de acceso de Adobe para comunicarse con dispositivos HSM. Si planea utilizar un HSM, utilice una versión de 32 bits de Java o un JDK que admita las interfaces PKCS11 completas.
