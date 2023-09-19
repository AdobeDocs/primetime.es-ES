---
title: Configuración de HSM
description: Configuración de HSM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Configuración de HSM {#hsm-configuration}

Si decide utilizar un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un [!DNL pkcs11.cfg] archivo de configuración. Este archivo debe encontrarse en el *LicenseServer.ConfigRoot* directorio. Consulte la [!DNL Adobe Access Server for Protected Streaming/configs] en el DVD de Adobe Access para un archivo de configuración PKCS11 de ejemplo. Para obtener información sobre el formato de [!DNL pkcs11.cfg], consulte la documentación del proveedor de Sun PKCS11.

Para comprobar que el archivo de configuración de HSM y Sun PKCS11 está configurado correctamente, puede utilizar el siguiente comando desde el directorio donde se encuentra el [!DNL pkcs11.cfg] el archivo se encuentra en ( [!DNL keytool] se instala con Java (JRE y JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente y el servidor de licencias podrá acceder a las credenciales.

>[!NOTE]
>
>En la actualidad, el servidor de acceso a Adobe para streaming protegido no admite HSM en sistemas operativos Windows de 64 bits.
