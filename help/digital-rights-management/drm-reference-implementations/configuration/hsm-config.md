---
description: Puede configurar la implementación de referencia con el proveedor Sun PKCS#11 que admite HSM. Aunque no se requiere el uso de un HSM, se recomienda.
title: Configuración de HSM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Configuración de HSM{#hsm-configuration}

Puede configurar la implementación de referencia con el proveedor Sun PKCS#11 que admite HSM. Aunque no se requiere el uso de un HSM, se recomienda.

Para utilizar una credencial en un HSM, debe crear un archivo de configuración para el proveedor Sun PKCS#11. Para obtener más información, consulte la [Guía de referencia de Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Para comprobar que los archivos de configuración HSM y Sun PKCS#11 están configurados, escriba el siguiente comando utilizando la herramienta clave que se instaló con el JDK de Java:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Ha configurado el HSM correctamente si puede ver sus credenciales en la lista.

>[!NOTE]
>
>A partir de Java 1.7, Sun Java de 64 bits para Windows ya no es compatible con las interfaces PKCS#11 que Adobe Primetime DRM requiere para comunicarse con dispositivos HSM. Si planea utilizar un HSM, asegúrese de utilizar una versión de 32 bits de Java o un JDK compatible con las interfaces PKCS#11 completas.
