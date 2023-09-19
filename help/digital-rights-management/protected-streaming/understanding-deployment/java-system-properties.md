---
description: Existen varias propiedades del sistema Java que puede configurar en el servidor de licencias para controlar la ubicación de los archivos de configuración y registro.
title: Propiedades del sistema Java
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Propiedades del sistema Java{#java-system-properties}

Existen varias propiedades del sistema Java que puede configurar en el servidor de licencias para controlar la ubicación de los archivos de configuración y registro.

Si lo desea, puede configurar las siguientes propiedades del sistema Java:

* *`LicenseServer.ConfigRoot`* — Nombre del directorio que incluye los ficheros de configuración del servidor de licencias.

  Consulte *Archivos de configuración del servidor de licencias* para obtener más información sobre el contenido de estos archivos. Si no se configura, el valor predeterminado es `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* — Nombre de la [!DNL logs] directorio en el que se encuentran los registros de la aplicación del servidor de licencias. Si no ha modificado el nombre de este directorio, el nombre de este directorio se configura como *LicenseServer.ConfigRoot* de forma predeterminada.

Si usa el [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, puede configurar las propiedades del sistema con la variable `JAVA_OPTS` variable de entorno. Las opciones de Java que configure se aplican automáticamente al iniciar Tomcat.

Por ejemplo, puede configurar la variable `JAVA_OPTS` como se indica a continuación:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
