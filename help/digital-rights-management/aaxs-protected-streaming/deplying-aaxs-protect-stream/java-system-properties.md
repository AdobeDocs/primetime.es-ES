---
seo-title: Propiedades del sistema Java
title: Propiedades del sistema Java
uuid: ad1f3d9b-7d95-4e19-a0f8-fd7d4dd4dc32
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Propiedades del sistema Java {#java-system-properties}

Opcionalmente, se pueden establecer las dos siguientes propiedades del sistema Java para modificar la ubicación de los archivos de configuración y registro para el servidor de licencias:

* *LicenseServer.ConfigRoot* — Directorio que contiene todos los archivos de configuración del servidor de licencias. Para obtener más información sobre el contenido de estos archivos, consulte &quot;Archivos[de configuración del servidor de](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)licencias&quot;. Si no se establece, el valor predeterminado es *CATALINA_BASE/licenciseserver*.
* *LicenseServer.LogRoot* — Directorio de la carpeta &quot;logs&quot;, donde se escriben los registros de la aplicación del servidor de licencias. Si no se establece, el valor predeterminado es *LicenseServer.ConfigRoot*.

Si utiliza [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, estas propiedades del sistema se pueden establecer fácilmente con la variable `JAVA_OPTS` environment. Cualquier opción de Java configurada aquí se utilizará cuando se inicie Tomcat. Por ejemplo, set:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

