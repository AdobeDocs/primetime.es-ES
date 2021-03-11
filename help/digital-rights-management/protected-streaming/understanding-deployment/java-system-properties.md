---
description: Hay varias propiedades del sistema Java que puede configurar en el servidor de licencias para controlar la ubicación de los archivos de configuración y registro.
title: Propiedades del sistema Java
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Propiedades del sistema Java{#java-system-properties}

Hay varias propiedades del sistema Java que puede configurar en el servidor de licencias para controlar la ubicación de los archivos de configuración y registro.

Si lo desea, puede configurar las siguientes propiedades del sistema Java:

* *`LicenseServer.ConfigRoot`* — Nombre del directorio que incluye los archivos de configuración del servidor de licencias.

   Consulte *Archivos de configuración del servidor de licencias* para obtener más información sobre el contenido de estos archivos. Si no se configura, el valor predeterminado es `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot*  — Nombre del  [!DNL logs] directorio en el que se ubican los registros de aplicaciones del servidor de licencias. Si no ha modificado el nombre de este directorio, el nombre de este directorio está configurado como *LicenseServer.ConfigRoot* de forma predeterminada.

Si utiliza el archivo [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, puede configurar las propiedades del sistema con la variable de entorno `JAVA_OPTS`. Las opciones de Java que configure se aplican automáticamente cuando se inicia Tomcat.

Por ejemplo, puede configurar la variable de entorno `JAVA_OPTS` de la siguiente manera:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

