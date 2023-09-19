---
description: Si selecciona un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración pkcs11.cfg.
title: Configuración de HSM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Configuración de HSM{#hsm-configuration}

Si selecciona un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración pkcs11.cfg.

Debe localizar el archivo de configuración en la *LicenseServer.ConfigRoot* directorio.

Consulte la [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] en el DVD de Adobe Primetime DRM para un archivo de configuración PKCS11 de ejemplo.

Consulte la documentación del proveedor de Sun PKCS11 sobre el formato de [!DNL pkcs11.cfg] archivo.

Puede utilizar el siguiente comando desde el directorio donde la variable [!DNL pkcs11.cfg] el archivo se encuentra en ( [!DNL keytool] se instala con Java (JRE y JDK) para comprobar que el archivo de configuración de HSM y Sun PKCS11 se ha configurado correctamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si puede ver las credenciales en la lista, el HSM estará configurado correctamente y el servidor de licencias podrá acceder a las credenciales.
