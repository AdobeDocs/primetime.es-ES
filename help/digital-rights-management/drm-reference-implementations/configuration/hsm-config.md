---
description: Puede configurar la implementación de referencia con el proveedor PKCS#11 de Sun que admite HSM. Aunque no se requiere el uso de un HSM, se recomienda.
seo-description: Puede configurar la implementación de referencia con el proveedor PKCS#11 de Sun que admite HSM. Aunque no se requiere el uso de un HSM, se recomienda.
seo-title: Configuración de HSM
title: Configuración de HSM
uuid: 2741ac40-aa42-4aa7-9864-037f3ed3dee2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Configuración de HSM{#hsm-configuration}

Puede configurar la implementación de referencia con el proveedor PKCS#11 de Sun que admite HSM. Aunque no se requiere el uso de un HSM, se recomienda.

Para utilizar una credencial en un HSM, debe crear un archivo de configuración para el proveedor PKCS#11 de Sun. Para obtener más información, consulte la Guía de referencia [Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Para verificar que el archivo de configuración HSM y Sun PKCS#11 está configurado, escriba el siguiente comando utilizando la herramienta clave que se instaló con el JDK de Java:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Ha configurado el HSM correctamente si puede vista sus credenciales en la lista.

>[!NOTE]
>
>A partir de Java 1.7, Sun Java de 64 bits para Windows ya no admite las interfaces PKCS#11 que Adobe Primetime DRM requiere para comunicarse con dispositivos HSM. Si planea utilizar un HSM, asegúrese de utilizar una versión de 32 bits de Java o un JDK que admita las interfaces PKCS#11 completas.

