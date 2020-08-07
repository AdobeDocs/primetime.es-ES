---
seo-title: Configuración de HSM
title: Configuración de HSM
uuid: 1cc5be99-c24c-4c1e-9348-fb69f96d8ca5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Configuración de HSM {#hsm-configuration}

No se requiere el uso de un HSM, pero se recomienda. La implementación de referencia se puede configurar para utilizar el proveedor PKCS11 de Sun para la compatibilidad con HSM. Para utilizar una credencial en un HSM, debe crear un archivo de configuración para el proveedor PKCS11 de Sun. Consulte la documentación de Sun para obtener más información. Para verificar que el archivo de configuración de HSM y Sun PKCS11 está configurado correctamente, puede utilizar el siguiente comando (keytool se instala con el JDK de Java):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente.

>[!NOTE]
>
>Desde Java 1.7, Sun Java de 64 bits para Windows no admite las interfaces PKCS11 que requiere Adobe Access DRM para comunicarse con dispositivos HSM. Si planea utilizar un HSM, utilice una versión de 32 bits de Java o un JDK que admita las interfaces PKCS11 completas.

