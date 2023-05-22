---
title: Propiedades del sistema Java
description: Propiedades del sistema Java
copied-description: true
exl-id: 3fac8fac-7c71-4638-a671-eecc203dc871
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Propiedades del sistema Java {#java-system-properties}

Las dos propiedades siguientes del sistema Java se pueden definir opcionalmente para modificar la ubicación de los ficheros de configuración y registro para el servidor de licencias:

* *LicenseServer.ConfigRoot* — Directorio que contiene todos los ficheros de configuración del servidor de licencias. Para obtener más información sobre el contenido de estos archivos, consulte[Archivos de configuración del servidor de licencias](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Si no se configura, el valor predeterminado es *CATALINA_BASE/licenseServer*.
* *LicenseServer.LogRoot* — Directorio de la carpeta &quot;logs&quot;, donde se escriben los registros de aplicación del servidor de licencias. Si no se configura, el valor predeterminado es *LicenseServer.ConfigRoot*.

Si está utilizando [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, estas propiedades del sistema se pueden configurar fácilmente con la variable `JAVA_OPTS` variable de entorno. Cualquier opción de Java establecida aquí se utilizará cuando se inicie Tomcat. Por ejemplo, establezca:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
