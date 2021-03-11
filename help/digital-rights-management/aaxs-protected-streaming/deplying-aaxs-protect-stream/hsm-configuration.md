---
title: Configuración de HSM
description: Configuración de HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Configuración de HSM {#hsm-configuration}

Si decide utilizar un HSM para almacenar sus credenciales de servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración [!DNL pkcs11.cfg]. Este archivo debe encontrarse en el directorio *LicenseServer.ConfigRoot*. Consulte el directorio [!DNL Adobe Access Server for Protected Streaming/configs] en el DVD de acceso al Adobe para ver un archivo de configuración PKCS11 de ejemplo. Para obtener información sobre el formato de [!DNL pkcs11.cfg], consulte la documentación del proveedor Sun PKCS11.

Para comprobar que el archivo de configuración HSM y Sun PKCS11 está configurado correctamente, puede utilizar el siguiente comando desde el directorio en el que se encuentra el archivo [!DNL pkcs11.cfg] ( [!DNL keytool] está instalado con Java JRE y JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente y el servidor de licencias podrá acceder a las credenciales.

>[!NOTE]
>
>El servidor de acceso a Adobe para transmisión protegida actualmente no admite HSM en sistemas operativos Windows de 64 bits.
