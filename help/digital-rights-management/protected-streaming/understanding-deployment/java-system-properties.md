---
description: Existen varias propiedades del sistema Java que puede configurar en el servidor de licencias para controlar la ubicación de los archivos de configuración y registro.
seo-description: Existen varias propiedades del sistema Java que puede configurar en el servidor de licencias para controlar la ubicación de los archivos de configuración y registro.
seo-title: Propiedades del sistema Java
title: Propiedades del sistema Java
uuid: d8c72359-bf61-47e0-9cd5-b21225d5fe49
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Propiedades del sistema Java{#java-system-properties}

Existen varias propiedades del sistema Java que puede configurar en el servidor de licencias para controlar la ubicación de los archivos de configuración y registro.

Opcionalmente, puede configurar las siguientes propiedades del sistema Java:

* *`LicenseServer.ConfigRoot`* — Nombre del directorio que incluye los archivos de configuración para el servidor de licencias.

   Consulte *Archivos de configuración del servidor de licencias* para obtener más información sobre el contenido de estos archivos. Si no se configura, el valor predeterminado es `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* — Nombre del  [!DNL logs] directorio en el que se ubican los registros de la aplicación del servidor de licencias. Si no ha modificado el nombre de este directorio, el nombre de este directorio se configura como *LicenseServer.ConfigRoot* de forma predeterminada.

Si utiliza el archivo [!DNL catalina.bat] o [!DNL catalina.sh] en inicio Tomcat, puede configurar las propiedades del sistema con la variable de entorno `JAVA_OPTS`. Todas las opciones de Java que configure se aplicarán automáticamente cuando Tomcat inicio.

Por ejemplo, puede configurar la variable de entorno `JAVA_OPTS` de la siguiente manera:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

