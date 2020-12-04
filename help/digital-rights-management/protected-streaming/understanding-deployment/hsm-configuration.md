---
description: Si selecciona un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración pkcs11.cfg.
seo-description: Si selecciona un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración pkcs11.cfg.
seo-title: Configuración de HSM
title: Configuración de HSM
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Configuración de HSM{#hsm-configuration}

Si selecciona un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración pkcs11.cfg.

Debe ubicar el archivo de configuración en el directorio *LicenseServer.ConfigRoot*.

Consulte el directorio [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] del DVD de Adobe Primetime DRM para ver un archivo de configuración PKCS11 de ejemplo.

Consulte la documentación del proveedor PKCS11 de Sun en relación con el formato del archivo [!DNL pkcs11.cfg].

Puede utilizar el siguiente comando del directorio en el que se encuentra el archivo [!DNL pkcs11.cfg] ( [!DNL keytool] se instala con Java JRE y JDK) para verificar que el archivo de configuración HSM y Sun PKCS11 se ha configurado correctamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si puede realizar la vista de sus credenciales en la lista, el HSM estará correctamente configurado y el servidor de licencias podrá acceder a las credenciales.
