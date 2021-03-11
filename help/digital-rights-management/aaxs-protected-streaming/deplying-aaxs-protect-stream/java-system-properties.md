---
title: Propiedades del sistema Java
description: Propiedades del sistema Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Propiedades del sistema Java {#java-system-properties}

Las dos propiedades del sistema Java siguientes se pueden configurar opcionalmente para modificar la ubicación de los archivos de configuración y registro para el servidor de licencias:

* *LicenseServer.ConfigRoot*  — Directorio que contiene todos los archivos de configuración del servidor de licencias. Para obtener más información sobre el contenido de estos archivos, consulte &quot;[Archivos de configuración del servidor de licencias](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Si no se establece, el valor predeterminado es *CATALINA_BASE/licenciseserver*.
* *LicenseServer.LogRoot*  — Directorio de la carpeta &quot;logs&quot;, donde se escriben los registros de la aplicación del servidor de licencias. Si no se establece, el valor predeterminado es *LicenseServer.ConfigRoot*.

Si utiliza [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, estas propiedades del sistema se pueden configurar fácilmente con la variable de entorno `JAVA_OPTS` . Cualquier opción de Java configurada aquí se utilizará cuando se inicie Tomcat. Por ejemplo, establezca:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

