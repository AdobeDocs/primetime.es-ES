---
description: Si selecciona un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración pkcs11.cfg.
title: Configuración de HSM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Configuración de HSM{#hsm-configuration}

Si selecciona un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración pkcs11.cfg.

Debe localizar el archivo de configuración en el directorio *LicenseServer.ConfigRoot*.

Consulte el directorio [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] en Adobe Primetime DRM DVD para ver un ejemplo de archivo de configuración PKCS11.

Consulte la documentación del proveedor Sun PKCS11 sobre el formato del archivo [!DNL pkcs11.cfg].

Puede utilizar el siguiente comando del directorio donde se encuentra el archivo [!DNL pkcs11.cfg] ( [!DNL keytool] está instalado con Java JRE y JDK) para verificar que el archivo de configuración HSM y Sun PKCS11 se haya configurado correctamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si puede ver sus credenciales en la lista, el HSM está configurado correctamente y el servidor de licencias ahora puede acceder a las credenciales.
