---
seo-title: Configuración de HSM
title: Configuración de HSM
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: ac75f63f98060e1937570476362bb5d4458d1f85
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Configuración de HSM {#hsm-configuration}

Si decide utilizar un HSM para almacenar sus credenciales de servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración [!DNL pkcs11.cfg]. Este archivo debe encontrarse en el directorio *LicenseServer.ConfigRoot*. Consulte el directorio [!DNL Adobe Access Server for Protected Streaming/configs] del DVD de Adobe Access para ver un archivo de configuración PKCS11 de ejemplo. Para obtener información sobre el formato de [!DNL pkcs11.cfg], consulte la documentación del proveedor PKCS11 de Sun.

Para verificar que el archivo de configuración de HSM y Sun PKCS11 está configurado correctamente, puede utilizar el siguiente comando desde el directorio donde se encuentra el archivo [!DNL pkcs11.cfg] ( [!DNL keytool] está instalado con Java JRE y JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente y el servidor de licencias podrá acceder a ellas.

>[!NOTE]
>
>Adobe Access Server para flujo continuo protegido no admite HSM en sistemas operativos Windows de 64 bits.
