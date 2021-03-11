---
description: Puede configurar la implementación de referencia con el proveedor de Sun PKCS#11 que admite HSM. Aunque el uso de un HSM no es obligatorio, se recomienda.
title: Configuración de HSM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Configuración de HSM{#hsm-configuration}

Puede configurar la implementación de referencia con el proveedor de Sun PKCS#11 que admite HSM. Aunque el uso de un HSM no es obligatorio, se recomienda.

Para utilizar una credencial en un HSM, debe crear un archivo de configuración para el proveedor de Sun PKCS#11. Para obtener más información, consulte la [Guía de referencia de Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Para comprobar que el archivo de configuración HSM y Sun PKCS#11 está configurado, escriba el siguiente comando utilizando la herramienta clave instalada con el JDK de Java:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Ha configurado el HSM correctamente si puede ver sus credenciales en la lista.

>[!NOTE]
>
>Desde Java 1.7, Sun Java de 64 bits para Windows ya no admite las interfaces PKCS#11 que Adobe Primetime DRM requiere para comunicarse con dispositivos HSM. Si planea utilizar un HSM, asegúrese de utilizar una versión de Java de 32 bits o un JDK que admita las interfaces PKCS#11 completas.

